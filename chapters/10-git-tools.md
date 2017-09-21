Git 与 GitHub 工具推荐
===

至于我的日常用的 Git 观看工具，一个是 WebStorm 和 Intellij IDEA 自带的，一个则是 SourceTree。

由于日常用的开发工是 Intellij IDEA 企业版，所以就有点依赖于这个工具了。最常用的功能便是：**修复 Bug 时，对于文件修改的追溯**。了解某行代码修改的原因，对应的修改人等等。

而 SourceTree 则方便用来查看一些非我写的项目，寻找其中的一些问题。个中缘由便是：**Intelli IDEA 刚打开某个项目的时候，需要花费大量的时间 index**，只可惜现有的 SourceTree 客户端都需要登录 Atlassian 账户了。

Git 命令行增强
---

### [diff-so-fancy](https://github.com/so-fancy/diff-so-fancy)

![diff so fancy 截图](git-diff-screenshot.png)

### [git-extras](https://github.com/tj/git-extras)

**Ubuntu**

```
$ sudo apt-get install git-extras
```

**Mac OS X with Homebrew**

```
$ brew install git-extras
```

```
$ git-summary


 project  : github-roam
 repo age : 2 years, 7 months
 active   : 40 days
 commits  : 124
 files    : 101
 authors  :
    72	Fengda HUANG  58.1%
    29	Fengda Huang  23.4%
     8	Phodal HUANG  6.5%
     3	Phodal Huang  2.4%
     2	yangpei3720   1.6%
     2	WangXiaolong  1.6%
     2	TZS           1.6%
     1	安正超        0.8%
     1	Li            0.8%
     1	Qiuer         0.8%
     1	SCaffrey      0.8%
     1	oncealong     0.8%
     1	zminds        0.8%
```

Intellij IDEA
---

Intellij IDEA

Git、GitHub桌面增强
---

### SourceTree

gitflow 分支合并、查看

![SourceTree 截图](sourcetree.jpg)

### GitHub Desktop

![GitHub Desktop](github-desktop.jpg)

Git 娱乐
---

### githug

```
$ githug 

********************************************************************************
*                                    Githug                                    *
********************************************************************************
No githug directory found, do you wish to create one? [yn]  y
Welcome to Githug!

Name: init
Level: 1
Difficulty: *

A new directory, `git_hug`, has been created; initialize an empty repository in it.
```


```
$ githug play                                                                                              

********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!

Name: config
Level: 2
Difficulty: *

Set up your git name and email, this is important so that your commits can be identified.
```

```
#1: init
#2: config
#3: add
#4: commit
#5: clone
#6: clone_to_folder
#7: ignore
#8: include
#9: status
#10: number_of_files_committed
#11: rm
#12: rm_cached
#13: stash
#14: rename
#15: restructure
#16: log
#17: tag
#...
```

### Gource

![Gource 历史](gource.jpg)
