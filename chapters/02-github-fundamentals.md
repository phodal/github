# Git基本知识与GitHub使用

## Git

从一般开发者的角度来看，git有以下功能：

1. 从服务器上克隆数据库（包括代码和版本信息）到单机上。
2. 在自己的机器上创建分支，修改代码。
3. 在单机上自己创建的分支上提交代码。
4. 在单机上合并分支。
5. 新建一个分支，把服务器上最新版的代码fetch下来，然后跟自己的主分支合并。
6. 生成补丁（patch），把补丁发送给主开发者。
7. 看主开发者的反馈，如果主开发者发现两个一般开发者之间有冲突（他们之间可以合作解决的冲突），就会要求他们先解决冲突，然后再由其中一个人提交。如果主开发者可以自己解决，或者没有冲突，就通过。
8. 一般开发者之间解决冲突的方法，开发者之间可以使用pull 命令解决冲突，解决完冲突之后再向主开发者提交补丁。

从主开发者的角度（假设主开发者不用开发代码）看，git有以下功能：

1. 查看邮件或者通过其它方式查看一般开发者的提交状态。
2. 打上补丁，解决冲突（可以自己解决，也可以要求开发者之间解决以后再重新提交，如果是开源项目，还要决定哪些补丁有用，哪些不用）。
3. 向公共服务器提交结果，然后通知所有开发人员。

### Git初入

如果是第一次使用Git，你需要设置署名和邮箱：

```
$ git config --global user.name "用户名"
$ git config --global user.email "电子邮箱"
```

将代码仓库clone到本地，其实就是将代码复制到你的机器里，并交由Git来管理：

```
$ git clone git@github.com:someone/symfony-docs-chs.git
```
    
你可以修改复制到本地的代码了（symfony-docs-chs项目里都是rst格式的文档）。当你觉得完成了一定的工作量，想做个阶段性的提交：

向这个本地的代码仓库添加当前目录的所有改动：

```
$ git add .
```
    
或者只是添加某个文件：

```
$ git add -p
````

我们可以输入

```
$git status
```

来看现在的状态，如下图是添加之前的：

![Before add](./img/before-add.png)

下面是添加之后 的

![After add](./img/after-add.png)

可以看到状态的变化是从黄色到绿色，即unstage到add。


## GitHub

Wiki百科上是这么说的

> GitHub 是一个共享虚拟主机服务，用于存放使用Git版本控制的软件代码和内容项目。它由GitHub公司（曾称Logical Awesome）的开发者Chris Wanstrath、PJ Hyett和Tom Preston-Werner
使用Ruby on Rails编写而成。

当然让我们看看官方的介绍：

> GitHub is the best place to share code with friends, co-workers, classmates, and complete strangers. Over eight million people use GitHub to build amazing things together.


它还是什么?

- 网站
- 免费博客
- 管理配置文件
- 收集资料
- 简历
- 管理代码片段
- 托管编程环境
- 写作

等等。看上去像是大餐，但是你还需要了解点什么?

### 版本管理与软件部署

jQuery[^jQuery]在发布版本``2.1.3``，一共有152个commit。我们可以看到如下的提交信息：

 - Ajax: Always use script injection in globalEval …	 bbdfbb4
 - Effects: Reintroduce use of requestAnimationFrame …	 72119e0
 - Effects: Improve raf logic …	 708764f
 - Build: Move test to appropriate module	 fbdbb6f
 - Build: Update commitplease dev dependency
 - ...

### GitHub与Git

> Git是一个分布式的版本控制系统，最初由Linus Torvalds编写，用作Linux内核代码的管理。在推出后，Git在其它项目中也取得了很大成功，尤其是在Ruby社区中。目前，包括Rubinius、Merb和Bitcoin在内的很多知名项目都使用了Git。Git同样可以被诸如Capistrano和Vlad the Deployer这样的部署工具所使用。

> GitHub可以托管各种git库，并提供一个web界面，但与其它像 SourceForge或Google Code这样的服务不同，GitHub的独特卖点在于从另外一个项目进行分支的简易性。为一个项目贡献代码非常简单：首先点击项目站点的“fork”的按钮，然后将代码检出并将修改加入到刚才分出的代码库中，最后通过内建的“pull request”机制向项目负责人申请代码合并。已经有人将GitHub称为代码玩家的MySpace。

### 在 GitHub 创建项目

接着,我们试试在上面创建一个项目：

![GitHub Roam](./img/github-roam-create.jpg)

就会有下面的提醒：

![GitHub Roam](./img/project-init.jpg)

它提供多种方式的创建方法：

> …or create a new repository on the command line

```
echo "# github-roam" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:phodal/github-roam.git
git push -u origin master
```
	
> …or push an existing repository from the command line

```
git remote add origin git@github.com:phodal/github-roam.git
git push -u origin master
```		
	
如果你完成了上面的步骤之后,那么我想你想知道你需要怎样的项目。

## GitHub 流行项目分析

之前曾经分析过一些GitHub的用户行为，现在我们先来说说GitHub上的Star吧。（截止：2015年3月9日23时。）

用户  | 项目名    | Language | Star | Url
-----|---------- |----------|------|----
twbs | Bootstrap | CSS      | 78490 | [https://github.com/twbs/bootstrap](https://github.com/twbs/bootstrap)
vhf |free-programming books | - | 37240 | [https://github.com/vhf/free-programming-books](https://github.com/vhf/free-programming-books)
angular | angular.js | JavaScript | 36,061 | [https://github.com/angular/angular.js](https://github.com/angular/angular.js)
mbostock | d3 | JavaScript | 35,257 | [https://github.com/mbostock/d3](https://github.com/mbostock/d3)
joyent | node | JavaScript | 35,077 | [https://github.com/joyent/node](https://github.com/joyent/node)

上面列出来的是前5的，看看大于1万个stars的项目的分布，一共有82个：

语言 | 项目数
-----|-----
JavaScript | 37
Ruby | 6 
CSS | 6 
Python | 4 
HTML | 3 
C++ | 3 
VimL | 2 
Shell | 2 
Go | 2 
C | 2 

类型分布：


 - 库和框架：如``jQuery`` 
 - 系统：如``Linux``、``hhvm``、``docker``
 - 配置集：如``dotfiles``
 - 辅助工具：如``oh-my-zsh``
 - 工具：如``Homewbrew``和``Bower``
 - 资料收集：如``free programming books``，``You-Dont-Know-JS``，``Font-Awesome``
 - 其他：简历如``Resume``
 
## Pull Request

除了创建项目之外，我们也可以创建Pull Request来做贡献。

### 我的第一个PR

我的第一个PR是给一个小的Node的CoAP相关的库的Pull Request。原因比较简单，是因为它的README.md写错了，导致我无法进行下一步。

		 const dgram       = require('dgram')
		-    , coapPacket  = require('coap-packet')
		+    , package     = require('coap-packet')

很简单，却又很有用的步骤，另外一个也是：

```
 else
   cat << END
 $0: error: module ngx_pagespeed requires the pagespeed optimization library.
-Look in obj/autoconf.err for more details.
+Look in objs/autoconf.err for more details.
 END
   exit 1
 fi
``` 

### CLA

CLA即Contributor License Agreement，在为一些大的组织、机构提交Pull Request的时候，可能需要签署这个协议。他们会在你的Pull Request里问你，只有你到他们的网站去注册并同意协议才会接受你的PR。

以下是我为Google提交的一个PR

![Google CLA](./img/google-cla.png)

以及Eclipse的一个PR

![Eclipse CLA](./img/eclipse-cla.png)

他们都要求我签署CLA。
