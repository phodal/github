#基本知识

##Git


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

###Git初入

如果是第一次使用Git，你需要设置署名和邮箱：

    $ git config --global user.name "用户名"
    $ git config --global user.email "电子邮箱"

将代码仓库clone到本地，其实就是将代码复制到你的机器里，并交由Git来管理：

    $ git clone git@github.com:someone/symfony-docs-chs.git
    
你可以修改复制到本地的代码了（symfony-docs-chs项目里都是rst格式的文档）。当你觉得完成了一定的工作量，想做个阶段性的提交：

向这个本地的代码仓库添加当前目录的所有改动：

    $ git add .
    
或者只是添加某个文件：

##Github

![Github Roam](../img/github-roam-create.jpg)

![Github Roam](../img/project-init.jpg)

多种方式

> …or create a new repository on the command line

    echo "# github-roam" >> README.md
	git init
	git add README.md
	git commit -m "first commit"
	git remote add origin git@github.com:phodal/github-roam.git
	git push -u origin master
	
> …or push an existing repository from the command line

	git remote add origin git@github.com:phodal/github-roam.git
	git push -u origin master
		
	