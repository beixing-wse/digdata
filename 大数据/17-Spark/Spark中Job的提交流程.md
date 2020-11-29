# Spark中Job的提交流程

## 提交作业

1. 行动算子

    ```scala
    resultRDD.collect().foreach(println)
    ```

2. 各种runJob

3. DAGScheduler 的 runJob 方法调用 submitJob 方法

    ```
    val waiter = submitJob(rdd, func, partitions, callSite, resultHandler, properties)
    ```

4. submitJob 方法中的将 Job 提交封装成一个 JobSubmitted 对象作为一个事件（event）放到 eventProcessLoop 中的 post 方法中

    ```scala
    eventProcessLoop.post(JobSubmitted(
          jobId, rdd, func2, partitions.toArray, callSite, waiter,
          SerializationUtils.clone(properties)))
    ```

5. post 方法中将事件放入到一个队列中并开启多线程进行处理

    ```
    def post(event: E): Unit = {
        eventQueue.put(event)
      }
    ```

6. 点击 eventQueue ，可见将 event 取出放到 onReceive 中接收

    ```
    val event = eventQueue.take()
              try {
                onReceive(event)
              } 
    ```

    在DAGSchedulerEventProcessLoop里面找到onReceive方法 ，调用 doOnReceive 对事件进行处理

    ```scala
    override def onReceive(event: DAGSchedulerEvent): Unit = {
        val timerContext = timer.time()
        try {
            doOnReceive(event)
        } finally {
            timerContext.stop()
        }
    }
    ```

7. doOnReceive 中对事件进行匹配，如果当前事件是 JobSubmitted 提交事件，调用 handleJobSubmitted 来处理作业提交。

    ```scala
    private def doOnReceive(event: DAGSchedulerEvent): Unit = event match {
        case JobSubmitted(jobId, rdd, func, partitions, callSite, listener, properties) =>
        dagScheduler.handleJobSubmitted(jobId, rdd, func, partitions, callSite, listener, properties)
        ...}
    ```

    

## 阶段划分

在 handleJobSubmitted 中有阶段的创建，job 的创建，阶段和 job 的关联。最终提交的不是 job，而是阶段。

- 阶段的创建

```scala
finalStage = createResultStage(finalRDD, func, partitions, jobId, callSite)
```

- job 的创建

```scala
val job = new ActiveJob(jobId, finalStage, callSite, listener, properties)
```

- stage 关联 job

```scala
finalStage.setActiveJob(job)
```

- 提交阶段

```scala
submitStage(finalStage)
```



点击 createResultStage 进入阶段的创建

**阶段创建具体步骤**

1. 阶段的创建，先去创建或者获取当前 RDD 的父 RDD 的阶段，这里的 parents 是一个 stage 的集合。

    ```scala
    val parents = getOrCreateParentStages(rdd, jobId)
    ```

2. getOrCreateParentStages 中对 RDD 调用 getShuffleDependencies 去获取当前 RDD 对应的宽依赖，getShuffleDependencies 只会将最近的宽依赖返回。然后对最近的宽依赖进行映射

    ```scala
    private def getOrCreateParentStages(rdd: RDD[_], firstJobId: Int): List[Stage] = {
        getShuffleDependencies(rdd).map { shuffleDep =>
            getOrCreateShuffleMapStage(shuffleDep, firstJobId)
        }.toList
    }
    ```

    **获取最近的宽依赖**：在 getShuffleDependencies 中将当前 RDD 压入栈中，去循环判断栈中是否为空，不为空则弹出，将RDD 设为已访问过的 RDD ，然后去遍历 RDD 的依赖关系，进行模式匹配，若是宽依赖则将宽依赖添加到 parents 中，若不是则将当前 RDD 的父 RDD 压入栈中继续循环。直到获取距当前 RDD 最近的宽依赖并将其返回。

    ```scala
    private[scheduler] def getShuffleDependencies(
        rdd: RDD[_]): HashSet[ShuffleDependency[_, _, _]] = {
      val parents = new HashSet[ShuffleDependency[_, _, _]]
      val visited = new HashSet[RDD[_]]
      val waitingForVisit = new Stack[RDD[_]]
      waitingForVisit.push(rdd)
      while (waitingForVisit.nonEmpty) {
        val toVisit = waitingForVisit.pop()
        if (!visited(toVisit)) {
          visited += toVisit
          toVisit.dependencies.foreach {
            case shuffleDep: ShuffleDependency[_, _, _] =>
              parents += shuffleDep
            case dependency =>
              waitingForVisit.push(dependency.rdd)
          }
        }
      }
      parents
    }
    ```

3. 最近宽依赖的映射方法（当前宽依赖的阶段还未创建）返回值是 stage，在该方法中去获取当前宽依赖的阶段进行模式匹配，未匹配到 stage ，调用getMissingAncestorShuffleDependencies 方法去获取当前宽依赖对应的其他宽依赖。

    ```scala
    private def getOrCreateShuffleMapStage(
          shuffleDep: ShuffleDependency[_, _, _],
          firstJobId: Int): ShuffleMapStage = {
        shuffleIdToMapStage.get(shuffleDep.shuffleId) match {
          case Some(stage) =>
            stage
    
          case None =>
            // Create stages for all missing ancestor shuffle dependencies.
            getMissingAncestorShuffleDependencies(shuffleDep.rdd).foreach { dep =>
              // Even though getMissingAncestorShuffleDependencies only returns shuffle dependencies
              // that were not already in shuffleIdToMapStage, it's possible that by the time we
              // get to a particular dependency in the foreach loop, it's been added to
              // shuffleIdToMapStage by the stage creation process for an earlier dependency. See
              // SPARK-13902 for more information.
              if (!shuffleIdToMapStage.contains(dep.shuffleId)) {
                createShuffleMapStage(dep, firstJobId)
              }
            }
            // Finally, create a stage for the given shuffle dependency.
            createShuffleMapStage(shuffleDep, firstJobId)
        }
      }
    ```

4. 获取其他宽依赖的方法 getMissingAncestorShuffleDependencies 

    ```scala
    private def getMissingAncestorShuffleDependencies(
          rdd: RDD[_]): Stack[ShuffleDependency[_, _, _]] = {
        val ancestors = new Stack[ShuffleDependency[_, _, _]]
        val visited = new HashSet[RDD[_]]
        // We are manually maintaining a stack here to prevent StackOverflowError
        // caused by recursively visiting
        val waitingForVisit = new Stack[RDD[_]]
        waitingForVisit.push(rdd)
        while (waitingForVisit.nonEmpty) {
          val toVisit = waitingForVisit.pop()
          if (!visited(toVisit)) {
            visited += toVisit
            getShuffleDependencies(toVisit).foreach { shuffleDep =>
              if (!shuffleIdToMapStage.contains(shuffleDep.shuffleId)) {
                ancestors.push(shuffleDep)
                waitingForVisit.push(shuffleDep.rdd)
              } // Otherwise, the dependency and its ancestors have already been registered.
            }
          }
        }
        ancestors
      }
    ```

    在该方法中同第二步中一样调用 getShuffleDependencies 方法去获取最近的宽依赖，不同的是再获取最近宽依赖后，会将当前 RDD 所依赖的父 RDD 压入栈中，循环的去获取宽依赖。获取完其他的宽依赖后回到 3 中的方法中调用 createShuffleMapStage 方法，去创建 stage 。

5.  createShuffleMapStage 方法，在该方法中通过宽依赖先去获取父 RDD ，通过父 RDD 去创建 ShuffleMapStage，并将 stage 返回。

    ```scala
    def createShuffleMapStage(shuffleDep: ShuffleDependency[_, _, _], jobId: Int): ShuffleMapStage = {
        val rdd = shuffleDep.rdd
        ...
        val stage = new ShuffleMapStage(id, rdd, numTasks, parents, jobId, rdd.creationSite, shuffleDep)
    
        stageIdToStage(id) = stage
        shuffleIdToMapStage(shuffleDep.shuffleId) = stage
        updateJobIdStageIdMaps(jobId, stage)
    
       ... ....
        stage
      }
    ```

6. 到此 parents 中的宽依赖的阶段就创建完毕了，再将 parents 传入到 ResultStage 中与最初的阶段结合形成最终的阶段，阶段数 = 宽依赖数  + 1 。在 createResultStage 中将阶段返回。

    ```scala
    private def createResultStage(
          rdd: RDD[_],
          func: (TaskContext, Iterator[_]) => _,
          partitions: Array[Int],
          jobId: Int,
          callSite: CallSite): ResultStage = {
        val parents = getOrCreateParentStages(rdd, jobId)
        val id = nextStageId.getAndIncrement()
        val stage = new ResultStage(id, rdd, func, partitions, parents, jobId, callSite)
        stageIdToStage(id) = stage
        updateJobIdStageIdMaps(jobId, stage)
        stage
      }
    ```

## Task任务的创建

在 handleJobSubmitted 中提交 finalStage，其实 stage 并不是提交的最细粒度，最细粒度是Task。

1. 进入 submitStage 中，获取阶段中的上级阶段，getMissingParentStages 返回一个 stage 的集合。

    进行判断，若上级阶段集合为空，通过 submitMissingTasks 将 stage 传入提交任务。若集合不为空，将上级阶段循环遍历提交阶段。

    ```scala
     private def submitStage(stage: Stage) {
        val jobId = activeJobForStage(stage)
        if (jobId.isDefined) {
          logDebug("submitStage(" + stage + ")")
          if (!waitingStages(stage) && !runningStages(stage) && !failedStages(stage)) {
            val missing = getMissingParentStages(stage).sortBy(_.id)
            logDebug("missing: " + missing)
            if (missing.isEmpty) {
              logInfo("Submitting " + stage + " (" + stage.rdd + "), which has no missing parents")
              submitMissingTasks(stage, jobId.get)
            } else {
              for (parent <- missing) {
                submitStage(parent)
              }
              waitingStages += stage
            }
          }
        } else {
          abortStage(stage, "No active job for stage " + stage.id, None)
        }
      }
    ```

2. 进入 submitMissingTasks 中，在 tasks 队列中进行模式匹配，分别创建 ShuffleMapTask 和 ResultTask

    任务数量由 partitionsToCompute 计算所得，每个分区对对应的 ShuffleMapTask 或 ResultTask，任务数等于阶段中最后一个 RDD 的分区数。

    ```scala
    val tasks: Seq[Task[_]] = try {
          stage match {
            case stage: ShuffleMapStage =>
              partitionsToCompute.map { id =>
                val locs = taskIdToLocations(id)
                val part = stage.rdd.partitions(id)
                new ShuffleMapTask(stage.id, stage.latestInfo.attemptId,
                  taskBinary, part, locs, stage.latestInfo.taskMetrics, properties, Option(jobId),
                  Option(sc.applicationId), sc.applicationAttemptId)
              }
    
            case stage: ResultStage =>
              partitionsToCompute.map { id =>
                val p: Int = stage.partitions(id)
                val part = stage.rdd.partitions(p)
                val locs = taskIdToLocations(id)
                new ResultTask(stage.id, stage.latestInfo.attemptId,
                  taskBinary, part, locs, id, properties, stage.latestInfo.taskMetrics,
                  Option(jobId), Option(sc.applicationId), sc.applicationAttemptId)
              }
          }
    ```

3. 分区数的计算

    ```scala
    val partitionsToCompute: Seq[Int] = stage.findMissingPartitions()
    ```

    ```scala
    val numPartitions = rdd.partitions.length
    ```

    此处的 rdd 为宽依赖的父 RDD（1.2中第5步可见）

    所以 task 数等于阶段中最后一个 rdd 的分区数。

4. 最终任务的提交

    ```scala
     if (tasks.size > 0) {
          logInfo("Submitting " + tasks.size + " missing tasks from " + stage + " (" + stage.rdd + ")")
          stage.pendingPartitions ++= tasks.map(_.partitionId)
          logDebug("New pending partitions: " + stage.pendingPartitions)
          taskScheduler.submitTasks(new TaskSet(
            tasks.toArray, stage.id, stage.latestInfo.attemptId, jobId, properties))
          stage.latestInfo.submissionTime = Some(clock.getTimeMillis())
        } 
    ```

    