[TOC]

# 1. 插件安装并连接

## 1.1、安装 SFTP

1. 用 ==Package Control== 安装插件
2. 按下Ctrl+Shift+P调出命令面板
3. 输入`install` 调出 `Install Package` 选项并回车，然后输入`sftp`，下拉列表中会出现一些相关的插件，选中sftp进行安装就行。
4. 插件安装过程可以查看 ==Sublime== 左下角的状态栏的信息。

> ==Sublime== 是一款强大的编辑器，它的强大体现在它强大的插件。
>
> 要实现 ==Sublime== 远程连接 ==Linux== 服务器，需要使用插件 ==SFTP==。



## 1.2、远程连接

### 1.2.1、基本连接

​		插件安装完成以后，需要进行配置。选菜单栏中的 ==File->SFTP/FTP->Set up Server==。这样就会打开一个配置文件：

![img](I:\课程\1 笔记\1.4 Markdown\(1) 计算机科学与技术\【3】大数据\Linux\img\SFTP配置.png)

​		我们需要配置一些远程连接的基本信息，如上图。远程IP、用户名、密码、打开目录。配置完成以后保存文件。

​		在选菜单栏中的 ==File->SFTP/FTP->Browse Server== 就可以看到自己配置的远程连接信息了，然后选中连接即可。然后就可以浏览远程服务器中的文件了。



### 1.2.2、同步文件夹（推荐）

​		先在本机 ==Windows== 下创建一个文件夹(最好使用英文)，使用 ==Sublime== 打开。此时，右键左侧 ==sidbar== 中这个文件图标，选择 ==SFTP/FTP: SFTP > Map to Remote…==。然后会打开一个.json的配置文件。我们需要在这个文件中配置连接需要的信息。同上面的配置。

![sublime连接linux](I:\课程\1 笔记\1.4 Markdown\(1) 计算机科学与技术\【3】大数据\Linux\img\sublime连接linux.png)

​		保存文件，右键文件图标，==SFTP > Download Folder==，就可以把远程文件夹的文件下载到同步的文件夹中了。以此类推，我们可以进行文件上传、同步等操作。

# 2、设置 linux 的格式

​		通常在 ==windows== 下写代码，然后通过 ==SVN== 或者直接 `copy` 到 ==linux== 下会有格式问题。比如 `^M` 的结束符问题，会造成 shell，c等代码不能正常运行。

通常可以用 ==vim== 在 ==linux== 端暴力解决：

```shell
# 会将该文件转成unix格式。
:set ff=unix
```

​		但这种方法应急或临时处理可以，但是不是长久之计。也不能每次创建文件都在 ==linux== 下创建，然后==svn== 管理。

​		当前我使用的是简单的编辑器 ==SublimeText2==，上网查了查， 找到了解决方法，让在 ==windows==下编辑，不改变 ==unix== 格式，或将已改变的文件转换为 ==unix== 模式。

**配置：**

1. 复制 ==Preferences -> Settings-Default== 里面的 `"default_line_ending"为"system"`到在 ==Preferences -> Settings-User== 里面并进行修改`"default_line_ending": "unix"`。
3. 手动操作 ==View -> Line Endings -> Unix==， 来改变当前项目或当前文件的文件结尾格式。