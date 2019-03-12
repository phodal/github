如何推广
===

除了擅长编写 md 电子书来攒 star，我还写了一系列的开源软件，也掌握了一些项目运营的技巧。

**开源并不是你把软件、README 写好就行了，还有详细的文档、示例程序等等**。

**开源也不是你的项目好了，就会有一堆人参与进来**。

**开源还要你帮助别人解决 Bug，……**。

**人们做事都是有原因的**，即动机。再举例一下，如果你的项目不够火，别人都没听过，那么**写到简历上可能没啥用**。

Marketing First
---

开源需要一些营销的技巧，这些技巧可以帮你吸引关注。举个简单的例子，司徒正美的 [avalon](https://github.com/RubyLouvre/avalon) 框架出身得很早，也 MV* 方面也做得很不错，但是在 marketing 上就……。以至于国内的很多前端，都不了解这个框架，要不今天在国内可能就是 AVRR 四大框架了。

Vue 不是因为好用，而一下子火了。这一点我印象特别深，当时在 GitHub Trending 上看到了这个项目，发现它还不能很好地 work。

而如文章 《[FIRST WEEK OF LAUNCHING VUE.JS](http://blog.evanyou.me/2014/02/11/first-week-of-launching-an-oss-project/)》所说，项目刚开始的时候作者做了一系列的营销计划：

 - HackerNews
 - Reddit /r/javascript
 - EchoJS
 - The DailyJS blog
 - JavaScript Weekly
 - Maintain a project Twitter account（维护项目的 Vue 账户）

除此，文中还提到了一篇文章《[How to Spread The Word About Your Code](https://hacks.mozilla.org/2013/05/how-to-spread-the-word-about-your-code/?utm_source=statuscode&utm_medium=email)》 。

这一点相当的有意思，如果你的想法好的话，那么大家都会肯定，点下链接，为你来个 star。那么，你就获得更好的动力去做这件事。项目也在开头的时候，获得了相当多的关注。而如果大家觉得你的项目没有新意的话，那么你懂的~。

除此，还有一种可能是，你的 ID 不够 fancy，即你在社区的影响上比较少。此时，就需要**一点点慢慢积累人气**了。当你积累了一些人气，你就能和松本行弘一样，在创建 mRuby 的时候就有 1000+ 的 star。并且，在社区上还有一些相关的文章介绍，各个头条也由他的粉丝发了上去。如，一年多以前，我创建了 [mole](https://github.com/phodal/mole) 项目。

![Mole](./img/mole.png)

当时，是为了给自己做一个基于 GitHub 云笔记的工具，在完成度到一定程度的时候。我在我的微信公从号上发了相关的介绍，第二天就有 100+ 的 star 了，还接收至最一些鼓舞的话语。对应于国内则有：

 - 极客头条
 - 掘金
 - 开发者头条
 - v2ex
 - 知乎
 - 不成器的微博

所以，你觉得呢？

编写一个好的 README
---

在一个开源项目里，README 是最重要的内容。它快速地介绍了这个项目，并决定了它能不能吸引用户：

 - **这个项目做什么？**
 - **它解决了什么问题**
 - **它有什么特性**
 - **hello, world 示例**

### 这个项目做什么——一句话文案

GitHub 的 Description 是我们在 Hacking News、GitHub Trneding 等等，第一时间看到的介绍。也是我们能快速介绍给别人的东西，如下图所示：

![GitHub Trending](./img/github-trending-example.png)

这一句话，必须简单明了也介绍，它是干什么的。

如 Angular 的一句话方案是：One framework. Mobile & desktop.

而 React 是：A declarative, efficient, and flexible JavaScript library for building user interfaces. 

Vue 则是：A progressive, incrementally-adoptable JavaScript framework for building UI on the web.

### 它解决了什么问题

上面的一句话描述，它不能很好地说明，它能解决什么问题。

如下是今天在 GitHub Trending 上榜的 RPC 项目的简介：

> Most machines on internet communicate with each other via TCP/IP. However TCP/IP only guarantees reliable data transmissions, we need to abstract more to build services:

![RPC 开源项目](./img/rpc-example.png)

以上便是这个项目能解决的问题，不过这个项目能解决的问题倒是比较长，哈哈哈。

### 它有什么特性

当我们有 A、B、C 几个不同的框架的时候，作为一个开发人员，就需要对比他们的特性。如下是 Go 语言实现的 MQTT 示例：

![GO MQTT 示例](./img/go-mqtt.png)

这个项目只支持的 Qos 级别为 0。如果我们需要的级别是 1，那么就不能用这个项目了。

又比如 lodash 项目：

> Lodash makes JavaScript easier by taking the hassle out of working with arrays,
numbers, objects, strings, etc. Lodash’s modular methods are great for:

 - Iterating arrays, objects, & strings
 - Manipulating & testing values
 - Creating composite functions

你会怎么写？脸皮够厚的话，可以直接写一下，与其它项目的对比，blabla：

![对比其它项目](./img/comparison.png)

当然了，这种事不能太过，要不然会招来一堆黑。

### 安装及hello, world 示例

在我们看完了上面的介绍之后，紧接着接一个 hello, world 的示例。在运行 hello, world 之前，我们可能需要一些额外的安装工作，如：

```
npm install koa
```

如 Koa 的示例：

```
const Koa = require('koa');
const app = new Koa();

// response
app.use(ctx => {
  ctx.body = 'Hello Koa';
});

app.listen(3000);
```

作为一个程序员，你应该懂得它的重要性。

好在这里的安装工作只有两步，而不是：

![Lan 安装过程](./img/lan-example.png)

对于那些需要复杂的安装过程的软件，应该简化安装过程，如提供 Docker 镜像，或者直接提供一个可运行的 Demo 环境。以免用户在看完 README 之后，直接放弃了使用该库。

技术文档
---

好了，依一个开发人员的角度，如果上面的步骤一切顺利的话，接下来，便是使用这个开源项目来完成我们的功能。这个时候，我们开始转移注意力到文档上了。

由于，之前在某一个项目，经历过一个第三方 API 文档的大坑——文档中只罗列了 API 的用法。如下 Intellij Idea 生成的结构图：

![API 示例](./img/api-examples.png)

文档中上，罗列了每个函数，以及每个函数需要的参数。我使用 Intellij Idea 直接反编译 jar 包，看到的信息都比文档多多了。文档上，没有任务示例，甚至连怎么初始化这个库的代码都没有。

WTF！

### 技术文档

对于一个复杂的开源项目来说，文档上要写明安装、编译、配置等等的过程。如下图所示：

![Python Social Auth 文档](./img/python-social-auth-example.png)

并且在我们发布包的时候，就要不断地去重复这个过程——如果你使用了自动化测试，那么这个过程便自动完成了。

如果我们的项目使用起来相当的简单，那么我们就可以只写一些示例代码即可。

并且，我们可以将文档直接入到代码里。它可以有效地减少文档不同步，带来的一些问题。

![Lodash 示例](./img/lodash-code-example.png)

上图是使用了 jsdoc 的 Lodash 示例。

除了上面的示例，我们还可以录制一些视频，写一些文章说明项目的思考、架构等等。

### 更多的示例程序

示例代码本身也是文档的一部分，不要问我为什么~~。

反正，除了一个 hello, world，你还要有各种场景下的示例：

![Redux](./img/redux-examples.png)

没有这么多示例，敢说自己是好用的开源项目？

### 编写技术文章、书籍

到目前为止，我们做了一系列 markdown 相关的工作，却也还没有结束。要知道只有真正写过一系列开源项目的人，才能体会到什么是 markdown 程序员~~。

官方文档，一般要以比较正式的口吻来描述过程，这种写法相当的压抑。如果要用轻松诙谐的口气，那么就可以写一系列的技术文章。假如这是一个前端框架，那么我们可以介绍它如何与某个后端框架配合使用；又或者是，它与某个框架的对比等等。

好了，一切顺利了，那么下一步就是吸引更多的人参与到项目上来了。

鼓励、吸引贡献者
---

要吸引其它开发人员来到你的项目，不是一件容易的事。

你需要不断地鼓励他/她们，并适时地帮他/她们解决问题，以避免他/她们在提 pull request 的过程中放弃了。这一点特别的有意思，当有一个开发人员发现了项目中的 bug，那么他/她会尝试去解决这个问题。与此同时，他/她还会为你的项目带来 pull request，但是在这个过程中，因为测试等等的问题，可能会阻碍他的 PR。这个时候，就需要我们主要去提示/教他们怎么做，又或者是帮他/她们解决完剩下的问题。那么，下次他/她提一个 PR 的时候，他/她就能解决问题了。

这一点可以在 README，以及介绍上体现：

![Feel free to contribute!](./img/feel-free-to.png)

哪怕只是一个错误字的 PR，那么你也可以 merge，啊哈哈~。然后，就有人帮你宣传了，『我给 xxx 项目一个 PR 了』。刚毕业的时候，我也是从这种类型的 PR 做起的~~。


