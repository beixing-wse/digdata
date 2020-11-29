# 简单配置Hadoop集群

- core-site.xml

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
    <!--
      Licensed under the Apache License, Version 2.0 (the "License");
      you may not use this file except in compliance with the License.
      You may obtain a copy of the License at
    
        http://www.apache.org/licenses/LICENSE-2.0
    
      Unless required by applicable law or agreed to in writing, software
      distributed under the License is distributed on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
      See the License for the specific language governing permissions and
      limitations under the License. See accompanying LICENSE file.
    -->
    
    <!-- Put site-specific property overrides in this file. -->
    
    <configuration>
    	<!-- hdfs默认的Namenode的地址 -->
    	<property>
            <name>fs.defaultFS</name>
            <value>hdfs://hadoop102:8020</value>
        </property>
        <!-- hadoop集群临时数据的路径 -->
        <property>
            <name>hadoop.tmp.dir</name>
            <value>/opt/module/hadoop-3.1.3/data</value>
        </property>
        <!-- 兼容性配置（Hive） -->
        <property>
            <name>hadoop.proxyuser.atguigu.hosts</name>
            <value>*</value>
        </property>
        <property>
            <name>hadoop.proxyuser.atguigu.groups</name>
            <value>*</value>
        </property>
        <property>
            <name>hadoop.http.staticuser.user</name>
            <value>atguigu</value>
        </property>
    
    </configuration>
    ```

- hdfs-site.xml

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
    <!--
      Licensed under the Apache License, Version 2.0 (the "License");
      you may not use this file except in compliance with the License.
      You may obtain a copy of the License at
    
        http://www.apache.org/licenses/LICENSE-2.0
    
      Unless required by applicable law or agreed to in writing, software
      distributed under the License is distributed on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
      See the License for the specific language governing permissions and
      limitations under the License. See accompanying LICENSE file.
    -->
    
    <!-- Put site-specific property overrides in this file. -->
    
    <configuration>
    	<!-- secondaryNamenode的地址 -->
    	<property>
            <name>dfs.namenode.secondary.http-address</name>
            <value>hadoop104:9868</value>
        </property>
    
    </configuration>
    
    ```

- yarn-site.xml

    ```xml
    <?xml version="1.0"?>
    <!--
      Licensed under the Apache License, Version 2.0 (the "License");
      you may not use this file except in compliance with the License.
      You may obtain a copy of the License at
    
        http://www.apache.org/licenses/LICENSE-2.0
    
      Unless required by applicable law or agreed to in writing, software
      distributed under the License is distributed on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
      See the License for the specific language governing permissions and
      limitations under the License. See accompanying LICENSE file.
    -->
    <configuration>
    
    <!-- Site specific YARN configuration properties -->
    	<property>
            <name>yarn.nodemanager.aux-services</name>
            <value>mapreduce_shuffle</value>
        </property>
        <!-- resourcemanager的路径 -->
        <property>
            <name>yarn.resourcemanager.hostname</name>
            <value>hadoop103</value>
        </property>
        <property>
            <name>yarn.nodemanager.env-whitelist</name>
            <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
        </property>
    
        <!-- 配置日志的聚集 -->
    	<property>
    		<name>yarn.log-aggregation-enable</name>
    		<value>true</value>
    	</property>
    	<property>
    		<name>yarn.log.server.url</name>
    		<value>http://${yarn.timelineservice.webapp.address}/applicationhistory/logs</value>
    	</property>
    	<property>
    		<name>yarn.log-aggregation.retain-seconds</name>
    		<value>604800</value>
    	</property>
    	<property>
    		<name>yarn.timeline-service.enabled</name>
    		<value>true</value>
    	</property>
    	<property>
    		<name>yarn.timeline-service.hostname</name>
    		<value>${yarn.resourcemanager.hostname}</value>
    	</property>
    	<property>
    		<name>yarn.timeline-service.http-cross-origin.enabled</name>
    		<value>true</value>
    	</property>
    	<property>
    		<name>yarn.resourcemanager.system-metricspublisher.enabled</name>
    		<value>true</value>
    	</property>
    
    </configuration>
    
    ```

- mapred-site.xml

    ```xml
    <?xml version="1.0"?>
    <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
    <!--
      Licensed under the Apache License, Version 2.0 (the "License");
      you may not use this file except in compliance with the License.
      You may obtain a copy of the License at
    
        http://www.apache.org/licenses/LICENSE-2.0
    
      Unless required by applicable law or agreed to in writing, software
      distributed under the License is distributed on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
      See the License for the specific language governing permissions and
      limitations under the License. See accompanying LICENSE file.
    -->
    
    <!-- Put site-specific property overrides in this file. -->
    
    <configuration>
    
    	<property>
            <name>mapreduce.framework.name</name>
            <value>yarn</value>
        </property>
    
    	<!-- 历史服务器端地址 -->
    	<property>
    		<name>mapreduce.jobhistory.address</name>
    		<value>hadoop102:10020</value>
    	</property>
    	<!-- 历史服务器 web 端地址 -->
    	<property>
    		<name>mapreduce.jobhistory.webapp.address</name>
    		<value>hadoop102:19888</value>
    	</property>
    
    	
    </configuration>
    
    ```

- workers

    ```
    hadoop102
    hadoop103
    hadoop104
    ```

    

    

    

    

    

    

    