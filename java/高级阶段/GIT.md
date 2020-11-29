# GIT

# 1、创建版本库并提交文件

- 查看git版本信息：`git --version`

- 设置用户名和邮箱

  - ```git
    git config --global user.name "your_username"
    git config --global user.email your_email@domain.com
    ```

-  查看所有配置：`git config --list`
- 初始化git本地仓库：`$ git init`
- 查看工作目录与暂存区文件状态：`git status`
- 添加文件到暂存区：`git add git01.txt(文件名)`
- 提交文件到本地版本库中：`git commit -m '(记录说明)'`

# 2、

- 查看日志：`git log` 	`git reflog`查看记录在本地的HEAD和分支引用在过去指向的位置。`git log --pretty=oneline`
- 查看本地文件与版本库文件的区别：`git diff HEAD -- git01.txt(文件名)`
- 撤销操作：`git reset Head (文件名)`
- 回退到上一版本：`git reset --hard HEAd^`
- 回退固定版本：`git reset --hard +(版本标识)`
- 文件误删除，重新检回：`git checkout --git01.txt(文件名)`
- 确定执行删除操作：`git rm git01.txt(文件名)`

# 3、远程仓库

- 获取远程仓库：`git clone (路径)`
- 将本地库推送到远程master主分支：`git push -u origin master`

# 4、分支操作

## 4.1本地分支创建、合并、重命名与删除

- 新建分支并切换到新建分支：`git checkout -b (分支名)`
- 切换到指定分支：`git checkout (分支名)`
- 删除指定分支：`git checkout -d (分支名)`
- 查看所有分支：`git branch`
- 合并分支（前提先切换到主分支master）：`git merge (分支名)`
- 重命名分支，如果newbranch名字分支已经存在，则需要使用-M强制重命名，否则，使用-m进行重命名：`git branch -m | -M oldbranch newbranch`

## 4.2分支Push与Pull操作

- 查看本地与远程分支：`git branch -a `
- 推送本地分支到远程：`git push origin (分支名)`
- 删除远程分支(本地分支还在保留)：`git push origin :remote_branch `
- 拉取远程指定分支并在本地创建分支:`git checkout -b local_branch origin/remote_branch `
- 拉取操作:`git pull`
- 提交操作：`git push`

# 5、标签管理

- 新建标签默认为HEAD:`git tag tag_name `
- 添加标签并指定标签描述信息:`git tag -a tag_name -m 'xxx' `
- 查看所有标签:`git tag`
- 删除一个本地标签:`git tag -d tag_name`
- 推送本地标签到远程:`git push origin tag_name`
- 推送全部未推送过的本地标签到远程:`git push origin --tags`
- 删除一个远程标签:`git push origin :refs/tags/tag_name `