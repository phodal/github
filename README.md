#GitHub 漫游指南

在线阅读: [GitHub 漫游指南](http://github.phodal.com/)

下载: [pdf](https://github.com/phodal/github-roam/raw/gh-pages/github-roam.pdf)、[mobi](https://github.com/phodal/github-roam/raw/gh-pages/github-roam.mobi)、[epub](https://github.com/phodal/github-roam/raw/gh-pages/github-roam.epub)

我的微信公众号：

![qrcode](./img/qrcode.jpg)

2014年，写了一个《[一步步搭建物联网系统](https://github.com/phodal/designiot)》。

2015.3.9号，想着写个《[GitHub漫游指南](http://github.phodal.com/)》，于是在最开始的地方写着：

> 我的GitHub主页上写着加入的时间——``Joined on Nov 8, 2010``，那时才大一，在那之后的那长日子里我都没有过到。也许是因为我学的不是计算机，到了今天——``2015.3.9``，我也发现这其实是程序员的社交网站。

但是过了很久都没有动静，今天是2015.10.24，我想是时候完成这个目标了。

##目录

<ul>
<li><a href="http://github.phodal.com/#前言">前言</a><ul>
<li><a href="http://github.phodal.com/#我与github的故事">我与GitHub的故事</a><ul>
<li><a href="http://github.phodal.com/#github与收获">GitHub与收获</a></li>
<li><a href="http://github.phodal.com/#github与成长">GitHub与成长</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#为什么你应该深入github">为什么你应该深入GitHub</a><ul>
<li><a href="http://github.phodal.com/#方便工作">方便工作</a></li>
<li><a href="http://github.phodal.com/#获得一份工作">获得一份工作</a></li>
<li><a href="http://github.phodal.com/#扩大交际">扩大交际</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#git基本知识与github使用">Git基本知识与GitHub使用</a><ul>
<li><a href="http://github.phodal.com/#git">Git</a><ul>
<li><a href="http://github.phodal.com/#git初入">Git初入</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#github">GitHub</a><ul>
<li><a href="http://github.phodal.com/#版本管理与软件部署">版本管理与软件部署</a></li>
<li><a href="http://github.phodal.com/#github与git">GitHub与Git</a></li>
<li><a href="http://github.phodal.com/#在github创建项目">在GitHub创建项目</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#github流行项目分析">GitHub流行项目分析</a></li>
<li><a href="http://github.phodal.com/#pull-request">Pull Request</a><ul>
<li><a href="http://github.phodal.com/#我的第一个pr">我的第一个PR</a></li>
<li><a href="http://github.phodal.com/#cla">CLA</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#构建github项目">构建GitHub项目</a><ul>
<li><a href="http://github.phodal.com/#如何用好github">如何用好GitHub</a><ul>
<li><a href="http://github.phodal.com/#敏捷软件开发">敏捷软件开发</a></li>
<li><a href="http://github.phodal.com/#测试">测试</a></li>
<li><a href="http://github.phodal.com/#ci">CI</a></li>
<li><a href="http://github.phodal.com/#代码质量">代码质量</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#模块分离与测试">模块分离与测试</a><ul>
<li><a href="http://github.phodal.com/#代码模块化">代码模块化</a></li>
<li><a href="http://github.phodal.com/#自动化测试">自动化测试</a></li>
<li><a href="http://github.phodal.com/#jshint">Jshint</a></li>
<li><a href="http://github.phodal.com/#mocha">Mocha</a></li>
<li><a href="http://github.phodal.com/#测试示例">测试示例</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#代码质量与重构">代码质量与重构</a><ul>
<li><a href="http://github.phodal.com/#code-climate">Code Climate</a></li>
<li><a href="http://github.phodal.com/#代码的坏味道">代码的坏味道</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#创建项目文档">创建项目文档</a><ul>
<li><a href="http://github.phodal.com/#readme">README</a></li>
<li><a href="http://github.phodal.com/#在线文档">在线文档</a></li>
<li><a href="http://github.phodal.com/#可用示例">可用示例</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#测试-1">测试</a><ul>
<li><a href="http://github.phodal.com/#tdd">TDD</a><ul>
<li><a href="http://github.phodal.com/#一次测试驱动开发">一次测试驱动开发</a></li>
<li><a href="http://github.phodal.com/#说说tdd">说说TDD</a></li>
<li><a href="http://github.phodal.com/#tdd思考">TDD思考</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#功能测试">功能测试</a><ul>
<li><a href="http://github.phodal.com/#轻量级网站测试twill">轻量级网站测试TWill</a></li>
<li><a href="http://github.phodal.com/#twill-登陆测试">Twill 登陆测试</a></li>
<li><a href="http://github.phodal.com/#twill-测试脚本">Twill 测试脚本</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#fake-server">Fake Server</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#重构">重构</a><ul>
<li><a href="http://github.phodal.com/#为什么重构">为什么重构?</a></li>
<li><a href="http://github.phodal.com/#重构umarkdown">重构uMarkdown</a><ul>
<li><a href="http://github.phodal.com/#代码说明">代码说明</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#interllij-idea重构">Interllij Idea重构</a><ul>
<li><a href="http://github.phodal.com/#rename">Rename</a></li>
<li><a href="http://github.phodal.com/#extract-method">Extract Method</a></li>
<li><a href="http://github.phodal.com/#inline-method">Inline Method</a></li>
<li><a href="http://github.phodal.com/#pull-members-up">Pull Members Up</a></li>
<li><a href="http://github.phodal.com/#重构之以查询取代临时变量">重构之以查询取代临时变量</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#如何在github寻找灵感fork">如何在GitHub“寻找灵感(fork)”</a><ul>
<li><a href="http://github.phodal.com/#lettuce构建过程"><a href="https://github.com/phodal/lettuce">Lettuce</a>构建过程</a><ul>
<li><a href="http://github.phodal.com/#需求">需求</a></li>
<li><a href="http://github.phodal.com/#计划">计划</a></li>
<li><a href="http://github.phodal.com/#实现第一个需求">实现第一个需求</a></li>
<li><a href="http://github.phodal.com/#实现第二个需求">实现第二个需求</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#github用户分析">GitHub用户分析</a><ul>
<li><a href="http://github.phodal.com/#生成图表">生成图表</a><ul>
<li><a href="http://github.phodal.com/#数据解析">数据解析</a></li>
<li><a href="http://github.phodal.com/#matplotlib">Matplotlib</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#每周分析">每周分析</a><ul>
<li><a href="http://github.phodal.com/#python-github-每周情况分析">python github 每周情况分析</a></li>
<li><a href="http://github.phodal.com/#python-数据分析">Python 数据分析</a></li>
<li><a href="http://github.phodal.com/#python-matplotlib图表">Python Matplotlib图表</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#存储到数据库中">存储到数据库中</a><ul>
<li><a href="http://github.phodal.com/#sqlite3">SQLite3</a></li>
<li><a href="http://github.phodal.com/#数据导入">数据导入</a></li>
<li><a href="http://github.phodal.com/#redis">Redis</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#邻近算法与相似用户">邻近算法与相似用户</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#github连击">GitHub连击</a><ul>
<li><a href="http://github.phodal.com/#天">100天</a><ul>
<li><a href="http://github.phodal.com/#天的提升">40天的提升</a></li>
<li><a href="http://github.phodal.com/#天的挑战">100天的挑战</a></li>
<li><a href="http://github.phodal.com/#天的希冀">140天的希冀</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#天的showcase">200天的Showcase</a><ul>
<li><a href="http://github.phodal.com/#一些项目简述">一些项目简述</a></li>
<li><a href="http://github.phodal.com/#google-map-solr-polygon-搜索">google map solr polygon 搜索</a></li>
<li><a href="http://github.phodal.com/#技能树">技能树</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#天-1">365天</a><ul>
<li><a href="http://github.phodal.com/#编程的基础能力">编程的基础能力</a></li>
<li><a href="http://github.phodal.com/#技术与框架设计">技术与框架设计</a></li>
<li><a href="http://github.phodal.com/#领域与练习">领域与练习</a></li>
<li><a href="http://github.phodal.com/#其他-1">其他</a></li>
</ul></li>
</ul></li>
</ul>

#前言

我的GitHub主页上写着加入的时间——``Joined on Nov 8, 2010``，那时才大一，在那之后的那长日子里我都没有过到。也许是因为我学的不是计算机，到了今天——``2015.3.9``，我也发现这其实是程序员的社交网站。

过去，曾经有很长的一些时间我试过在GitHub上连击，也试着去了解别人是如何用好这个工具的。当然粉丝在GitHub上也是很重要的。

在这里，我会试着将我在GitHub上学到的东西一一分享出来。

##我与GitHub的故事

在我大四找工作的时候，试图去寻找一份硬件、物联网相关的工作(ps: 专业是电子信息工程)。尽管简历上写得满满的各种经历、经验，然而并没有卵用。跑了几场校园招聘会后，十份简历(ps: 事先已经有心里准备)一个也没有投出去——因为学校直接被拒。我对霸面什么的一点兴趣都没有，千里马需要伯乐。后来，我加入了Martin Flower所在的公司，当然这是后话了。

这是一个残酷的世界，在学生时代，如果你长得不帅不高的话，那么多数的附加技能都是白搭(ps: 通常富的是看不到这篇文章的)。在工作时期，如果你上家没有名气，那么将会影响你下一份工作的待遇。而，很多东西却会改变这些，GitHub就是其中一个。

注册GitHub的时候大概是大一的时候，我熟悉的时候已经是大四了，现在已经毕业一年了。在过去的近两年里，我试着以几个维度在GitHub上创建项目:

1. 快速上手框架来实战，即demo
2. 重构别人的代码
3. 创建自己可用的框架
4. 快速构建大型应用
5. 构建通用的框架

###GitHub与收获

先说说**与技能无关的收获**吧，毕业设计做的是一个《[最小物联网系统](https://github.com/phodal/iot)》，考虑到我们专业老师没有这方面知识，答辩时会带来问题，尽量往这方面靠拢。当我毕业后，这个项目已经有过百个star了，这样易上手的东西还是比较受欢迎的(ps: 不过这种硬件相关的项目通常受限于GitHub上硬件开发工程师比较少的困扰)。

毕业后一个月收到PACKT出版社的邮件(ps: 他们是在github上找到我的)，内容是关于Review一本[物联网](iot)书籍，即在《[从Review到翻译IT书籍](http://www.phodal.com/blog/review-it-books-with-translate-book/)》中提到的《Learning Internet of Things》。作为一个四级没过的"物联网专家"，去审阅一本英文的物联网书籍。。。

当然，后来是审阅完了，书上有我的英文简介。

![Phodal Huang Introduction](./img/phodal-intro.jpg)

一个月前，收到MANNING出版社的邮件(ps: 也是在github上)，关于Review一本[物联网](iot)书籍的目录，并提出建议。

也因此带来了其他更多的东西，当然不是这里的主题。在这里，我们就不讨论各种骚扰邮件，或者中文合作。从没有想象过，我也可以在英语世界有一片小天地。

这些告诉我们，GitHub上找一个你擅长的主题，那么会有很多人找上你的。

###GitHub与成长

过去写过一篇《[如何通过github提升自己](http://www.phodal.com/blog/use-github-grow-self/)》的文章，现在只想说三点:

1. 测试
2. 更多的测试
3. 更多的、更多的、更多的测试

没有测试的项目是很扯淡的，除非你的项目只有一个函数，然后那个函数返回``Hello,World``。

如果你的项目代码有上千行，如果你能保证测试覆盖率可以达到95%以的话，那么我想你的项目不会有太复杂的函数。假使有这样的函数，那么他也是被测试覆盖住的。

如果你在用心做这个项目，那么你看到代码写得不好也会试着改进，即重构。当有了一些，你的技能会不断提升。你开始会试着接触更多的东西，如stub，如mock，如fakeserver。

有一天，你会发现你离不开测试。

然后就会相信: **那些没有写测试的项目都是在耍流氓**

##为什么你应该深入GitHub

上面我们说的都是我们可以收获到的东西，我们开始尝试就意味着我们知道它可能给我们带来好处。上面已经提到很多可以提升自己的例子了，这里再说说其他的。

###方便工作

我们可以从中获取到不同的知识、内容、信息。每个人都可以从别人的代码中学习，当我们需要构建一个库的时候我们可以在上面寻找不同的库和代码来实现我们的功能。如当我在实现一个库的时候，我会在GitHub上到相应的组件:

- Promise 支持
- Class类(ps:没有一个好的类使用的方式)
- Template 一个简单的模板引擎
- Router 用来控制页面的路由
- Ajax 基本的Ajax Get/Post请求

###获得一份工作

越来越多的人因为GitHub获得工作，因为他们的做的东西正好符合一些公司的要求。那么，这些公司在寻找代码的时候，就会试着邀请他们。

因而，在GitHub寻找合适的候选人，已经是一种趋势。

###扩大交际

如果我们想创造出更好、强大地框架时，那么认识更多的人可能会带来更多的帮助。有时候会同上面那一点一样的效果 

---

更多请见[GitHub 漫游指南](http://github.phodal.com/)

## License

![cc](https://i.creativecommons.org/l/by-nc/4.0/88x31.png)

本作品采用[知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/)进行许可。

© 2015 [Phodal Huang](http://www.phodal.com)。[待我代码编成，娶你为妻可好](http://www.xuntayizhan.com/person/ji-ke-ai-qing-zhi-er-shi-dai-wo-dai-ma-bian-cheng-qu-ni-wei-qi-ke-hao-wan/)。

