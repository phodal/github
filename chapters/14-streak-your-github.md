GitHub连击 
===

## 100天

我也是蛮拼的，虽然我想的只是在GitHub上连击100~200天，然而到了今天也算不错。

![Longest Streak](./img/longest-streak.png)

``在不停地造轮子的过程中，也不停地造车子。``

在那篇连续冲击365天的文章出现之前，我们公司的大大([https://github.com/dreamhead](https://github.com/dreamhead))也曾经在公司内部说过，天天commit什么的。当然这不是我的动力，在连击140天之前

- 给过google的``ngx_speed``、``node-coap``等项目创建过pull request
- 也有``free-programming-books``、``free-programming-books-zh_CN``这样的项目。
- 当然还有一个连击20天。

对比了一下365天连击的commit，我发现我在total上整整多了近0.5倍。

![365 Streak](./img/365-streak.jpg)

同时这似乎也意味着，我每天的commit数与之相比多了很多。

在连击20的时候，有这样的问题：*为了commit而commit代码*，最后就放弃了。

而现在是``为了填坑而commit``，为自己挖了太多的想法。

### 40天的提升

当时我需要去印度接受毕业生培训，大概有5周左右，想着总不能空手而归。于是在国庆结束后有了第一次commit，当时旅游归来，想着自己在不同的地方有不同的照片，于是这个repo的名字是 [onmap](https://github.com/phodal/onmap)——将自己的照片显示在地图上的拍摄地点(手机是Lumia 920)。然而，中间因为修改账号的原因，丢失了commit。

再从印度说起，当时主要维护三个repo：

- 物联网的CoAP协议
- [一步步设计物联网系统](https://github.com/phodal/designiot)的电子书
- 一个Node.js + JS的网站

说说最后一个，最后一个是练习的项目。因为当时培训比较无聊，业余时间比较多，英语不好，加上听不懂印度人的话。晚上基本上是在住的地方默默地写代码，所以当时的目标有这么几个：

- TDD
- 测试覆盖率
- 代码整洁

这也就是为什么那个repo有这样的一行：

![Repo Status](./img/repo-status.png)

做到98%的覆盖率也算蛮拼的，当然还有Code Climate也达到了4.0，也有了112个commits。因此也带来了一些提高：

- 提高了代码的质量(code climate比jslint更注重重复代码等等一些bad smell)。
- 对于Mock、Stub、FakesServer等用法有更好的掌握
- 可以持续地交付软件(版本管理、自动测试、CI、部署等等)

### 100天的挑战

(ps：从印度回来之后，由于女朋友在泰国实习，有了更多的时间可以看书、写代码)

有意思的是越到中间的一些时间，commits的次数上去了，除了一些简单的pull request，还有一些新的轮子出现了。

![Problem](./img/problem.jpg)

这是上一星期的commits，这也就意味着，在一星期里面，我需要在8个repo里切换。而现在我又有了一个新的idea，这时就发现了一堆的问题：

 - 今天工作在这个repo上，突然发现那个repo上有issue，需要去修复，于是就放下了当前的代码。
 - 在不同的repo间切换容易分散精力
 - 很容易就发现有太多的功能可以实现，但是时间是有限的。
 - 没有足够的空闲时间，除了周末。
 - 希望去寻找那些有兴趣的人，然而却发现原来没有那么多时间去找人。

### 140天的希冀

在经历了100天之后，似乎整个人都轻松了，毕竟目标是100~200天。似乎到现在，也不会有什么特殊的情怀，除了一些希冀。

当然，对于一个开源项目的作者来说，最好有下面的情况：

- 很多人知道了这个项目
- 很多人用它的项目。
- 在某些可以用这个项目快速解决问题的地方提到了这个项目
- 提了bug、issue、问题。
- 提了bug，并解决了。(ps：这是最理想的情况)


## 200天的Showcase

今天是我连续泡在GitHub上的第200天，也是蛮高兴的，终于到达了：

![GitHub 200 days](./img/github-200-days.png)

故事的背影是：去年国庆完后要去印度接受毕业生培训——就是那个神奇的国度。但是在去之前已经在项目待了九个多月，项目上的挑战越来越少，在印度的时间又算是比较多。便给自己设定了一个长期的goal，即100~200天的longest streak。

或许之前你看到过一篇文章[让我们连击](https://github.com/phodal/github-roam/blob/master/chapters/12-streak-your-github.md)，那时已然140天，只是还是浑浑噩噩。到了今天，渐渐有了一个更清晰地思路。

先让我们来一下ShowCase，然后再然后，下一篇我们再继续。

### 一些项目简述

上面说到的培训一开始是用Java写的一个网站，有自动测试、CI、CD等等。由于是内部组队培训，代码不能公开等等因素，加之做得无聊。顺手，拿Node.js +RESTify 做了Server，Backbone + RequireJS + jQuery 做了前台的逻辑。于是在那个日子里，也在维护一些旧的repo，如[iot-coap](https://github.com/phodal/iot-coap)、[iot](https://github.com/phodal/iot)，前者是我拿到WebStorm开源License的Repo，后者则是毕业设计。

对于这样一个项目也需要有测试、自动化测试、CI等等。CI用的是Travics-CI。总体的技术构架如下：

#### 技术栈

前台：

- Backbone 
- RequireJS
- Underscore
- Mustache
- Pure CSS

后台：

- RESTify

测试：

- Jasmine
- Chai
- Sinon
- Mocha
- Jasmine-jQuery

一直写到五星期的培训结束， 只是没有自动部署。想想就觉得可以用github-page的项目多好~~。

过程中还有一些有意思的小项目，如：

### google map solr polygon 搜索

[google map solr polygon 搜索](http://www.phodal.com/blog/google-map-width-solr-use-polygon-search/)

![google map solr](./img/solr.png)

代码：[https://github.com/phodal/gmap-solr](https://github.com/phodal/gmap-solr)

### 技能树

这个可以从两部分说起：

#### 重构 Skill Tree

原来的是

- Knockout
- RequireJS
- jQuery
- Gulp

![Skill Tree](./img/skilltree.jpg)

代码：[https://github.com/phodal/skillock](https://github.com/phodal/skillock)

#### 技能树Sherlock

- D3.js
- Dagre-D3.js
- jquery.tooltipster.js
- jQuery
- Lettuce
- Knockout.js
- Require.js

![Sherlock skill tree](./img/sherlock.png)

代码：[https://github.com/phodal/sherlock](https://github.com/phodal/sherlock)

#### Django Ionic ElasticSearch 地图搜索

![Django Elastic Search](./img/elasticsearch_ionit_map.jpg)

- ElasticSearch
- Django
- Ionic
- OpenLayers 3

代码：[https://github.com/phodal/django-elasticsearch](https://github.com/phodal/django-elasticsearch)

#### 简历生成器

![Resume](./img/resume.png)

- React
- jsPDF
- jQuery
- RequireJS
- Showdown

代码：[https://github.com/phodal/resume](https://github.com/phodal/resume)


#### Nginx 大数据学习

![Nginx Pig](./img/nginx_pig.jpg)

- ElasticSearch
- Hadoop
- Pig

代码：[https://github.com/phodal/learning-data/tree/master/nginx](https://github.com/phodal/learning-data/tree/master/nginx)
 
#### 其他

虽然技术栈上主要集中在Python、JavaScript，当然还有一些Ruby、Pig、Shell、Java的代码，只是我还是习惯用Python和JavaScript。一些用到觉得不错的框架：

- Ionic：开始Hybird移动应用。
- Django：Python Web开发利器。
- Flask：Python Web开发小刀。
- RequireJS：管理js依赖。
- Backbone：Model + View + Router。
- Angluar：...。
- Knockout：MVV*。
- React：据说会火。
- Cordova：Hybird应用基础。

还应该有

- ElasticSearch
- Solr
- Hadoop
- Pig
- MongoDB
- Redis

## 365天
  
> 给你一年的时间，你会怎样去提高你的水平？？？

![GitHub 365](./img/github-365.jpg)

正值这难得的sick leave（万恶的空气），码文一篇来记念一个过去的366天里。尽管想的是在今年里写一个可持续的开源框架，但是到底这依赖于一个好的idea。在我的[GitHub 孵化器](http://github.com/phodal/ideas) 页面上似乎也没有一个特别让我满意的想法，虽然上面有各种不样有意思的ideas。多数都是在过去的一年是完成的，然而有一些也是还没有做到的。

尽管一直在GitHub上连击看上去似乎是没有多大必要的，但是人总得有点追求。如果正是漫无目的，却又想着提高技术的同时，为什么不去试试？毕竟技术非常好、不需要太多练习的人只是少数，似乎这样的人是不存在的。大多数的人都是经过练习之后，才会达到别人口中的“技术好”。

这让我想起了充斥着各种气味的知乎上的一些问题，在一些智商被完虐的话题里，无一不是因为那些人学得比别人早——哪来的天才？所谓的天才，应该是未来的智能生命一般，一出生什么都知道。如果并非如此，那只是说明他练习到位了。

练习不到位便意味着，即使你练习的时候是一万小时的两倍，那也是无济于事的。如果你学得比别人晚，在**很长的一段时间里**(可能直到进棺材)输给别人是必然的——落后就要挨打。就好像我等毕业于一所二本垫底的学校里，如果在过去我一直保持着和别人(各种重点)一样的学习速度，那么我只能一直是Loser。

需要注意的是，对你来说考上二本很难，并不是因为你比别人笨。教育资源分配不均的问题，在某种程度上导致了新的阶级制度的出现。如[我的首页](https://www.phodal.com/)说的那样：**THE ONLY FAIR IS NOT FAIR**——唯一公平的是它是不公平的。我们可以做的还有很多——**CREATE & SHARE**。真正的不幸是，因为营养不良导致的教育问题。

于是在想明白了很多事的时候起，便有了Re-Practise这样的计划，而365天只是中间的一个产物。

### 编程的基础能力

虽说算法很重要，但是编码才是基础能力。算法与编程在某种程度上是不同的领域，算法编程是在编程上面的一级。算法写得再好，如果别人很难直接拿来复用，在别人眼里就是shit。想出能work的代码一件简单的事，学会对其重构，使之变得更易读就是一件有意义的事。

于是，在某一时刻在GitHub上创建了一个组织，叫[Artisan Stack](https://github.com/artisanstack)。当时想的是在GitHub寻找一些JavaScript项目，对其代码进行重构。但是到底是影响力不够哈，参与的人数比较少。

#### 重构

如果你懂得如何写出高可读的代码，那么我想你是不需要这个的，但是这意味着你花了更多的时候在思考上了。当谈论重构的时候，让我想起了TDD(测试驱动开发)。即使不是TDD，那么如果你写着测试，那也是可以重构的。(之前写过一些利用Intellij IDEA重构的文章：[提炼函数](https://www.phodal.com/blog/intellij-idea-refactor-extract-method/)、[以查询取代临时变量](https://www.phodal.com/blog/intellij-idea-refactor-replace-temp-with-query/)、[重构与Intellij Idea初探](https://www.phodal.com/blog/thoughtworks-refactor-and-intellij-idea/)、[内联函数](https://www.phodal.com/blog/intellij-idea-refactor-inline-method/))

在各种各样的文章里，我们看到过一些相关的内容，最好的参考莫过于《重构》一书。最基础不过的原则便是函数名，取名字很难，取别人能读懂的名字更难。其他的便有诸如长函数、过大的类、重复代码等等。在我有限的面试别人的经历里，这些问题都是最常见的。

#### 测试

而如果没有测试，其他都是扯淡。写好测试很难，写个测试算是一件容易的事。只是有些容易我们会为了测试而测试。

在我写[EchoesWorks](https://github.com/echoesworks/echoesworks)和[Lan](https://github.com/phodal/lan)的过程中，我尽量去保证足够高的测试覆盖率。

![lan](./img/lan.png)

![EchoesWorks](./img/echoesworks.png)

从测试开始的TDD，会保证方法是可测的。从功能到测试则可以提供工作次效率，但是只会让测试成为测试，而不是代码的一部分。

测试是代码的最后一公里。所以，尽可能的为你的GitHub上的项目添加测试。

#### 编码的过程

初到TW时，Pair时候总会有人教我如何开始编码，这应该也是一项基础的能力。结合日常，重新演绎一下这个过程：

1. 有一个可衡量、可实现、过程可测的目标
2. Tasking (即对要实现的目标过程进行分解)
3. 一步步实现 (如TDD)
4. 实现目标

放到当前的场景就是：

1. 我想在GitHub上连击365天。对应于每一个时候段的目标都应该是可以衡量、测试的——即每天都会有Contributions。
2. 分解就是一个痛苦的过程。理想情况下，我们应该会有每天提交，但是这取决于你的repo的数量，如果没有新的idea出现，那么这个就变成为了Contributions而Commit。
3. 一步步实现

在我们实际工作中也是如此，接到一个任务，然后分解，一步步完成。不过实现会稍微复杂一些，因为事务总会有抢占和优先级的。

### 技术与框架设计

在上上一篇博客中《[After 500：写了第500篇博客，然后呢?](https://www.phodal.com/blog/after-500-blogposts-analytics-after-tech/)》也深刻地讨论了下这个问题，技术向来都是后发者优势。对于技术人员来说，也是如此，后发者占据很大的优势。

如果我们只是单纯地把我们的关注点仅仅放置于技术上，那么我们就不具有任何的优势。而依赖于我们的编程经验，我们可以在特定的时候创造一些框架。而架构的设计本身就是一件有意思的事，大抵是因为程序员都喜欢创造。(ps：之前曾经写过这样一篇文章，《[对不起，我并不热爱编程，我只喜欢创造](https://www.phodal.com/blog/sorry-i-don't-like-programming/)》)

**创造是一种知识的再掌握过程。**

回顾一下写echoesworks的过程，一开始我需要的是一个网页版的PPT，当然这类的东西已经有很多了，如impress.js、bespoke.js等等。分析一下所需要的功能：markdown解析器、键盘事件处理、Ajax、进度条显示、图片处理、Slide。我们可以在GitHub上找到各式各样的模块，我们所要做的就是将之结合在一样。在那之前，我试着用类似的原理写（组合）了[Lettuce](https://github.com/phodal/lettuce)。

组合相比于创造过程是一个更有挑战性的过程，我们需要在这过程去设计胶水来粘合这些代码，并在最终可以让他工作。这好比是我们在平时接触到的任务划分，每个人负责相应的模块，最后整合。

我在写[lan](https://github.com/phodal/lan)的时候，也是类似的，但是不同的是我已经设计了一个清晰的架构图。

![Lan IoT](./img/lan-iot.jpg)

而在我们实现的编码过程也是如此，使用不同的框架，并且让他们能工作。如早期玩的[moqi.mobi](https://github.com/echoesworks/moqi.mobi)，基于Backbone、RequireJS、Underscore、Mustache、Pure CSS。在随后的时间里，用React替换了View层，就有了[backbone-react](https://github.com/phodal/backbone-react)的练习。

技术同人一样，需要不断地往高一级前进。我们只需要不断地Re-Practise。

### 领域与练习 

说业务好像不太适合程序员的口味，那就领域吧。不同行业的人，如百度、阿里、腾讯，他们的领域核心是不一样的。

而领域本身也是相似的，这可以解释为什么互联网公司都喜欢互相挖人，而一般都不会去华为、中兴等非互联网领域挖人。出了这个领域，你可能连个毕业生都不如。领域、业务同技术一样是不断强化知识的一个过程。Ritchie先实现了BCPL语言，而后设计了C语言，而BCPL语言一开始是基于CPL语言。

领域本身也在不断进化。

这也是下一个值得提高的地方。

### 其他

是时候写这个小结了。从不会写代码，到写代码是从0到1的过程，但是要从1到60都不是一件容易的事。无论是刷GitHub也好(不要是自动提交)，或者是换工作也好，我们都在不断地练习。

而练习是要分成不同的几个步骤，不仅仅局限于技术：

1. 编码
2. 架构
3. 设计
4. 。。。

---

## 500天

尽管之前已经有100天、200天、365天的文章，但是这不是一篇象征性的500天的文章。对这样的一个事物，每个人都会有不同听看法。有的会说这是一件好事，有的则不是。但是别人的看法终究不重要，因为了解你自己的只有你自己。别人都只是以他们的角度来提出观点。

在这500天里，我发现两点有意思的事，也是总结的时候才意识到的：

1. 编程的情绪周期
2. 有意图的练习

那么，当我们不断地练习的时候，我们就可以写出更好的代码。

我想你也听过一万小时天才理论的说法：要成为某个领域的专家，需要10000小时。而在这其中最重要的一点是有意图的练习——而不是一直重复性地用不同的语言去写一个相同的算法。如果我们有一天8小时的工作时间  + 2 小时的提高时间，那么我们还是需要1000天才能实现一万小时。

### 500天与10000小时

当然如果你连做梦也在写代码的话，那么我想500天就够了，哈哈~~。

![Gtihub 500](./img/github-500.jpg)

虽然不是连击次数最多的，但是根据[Most active GitHub users ](http://git.io/top)的结果来说，好似是大陆提交数最多的人，没有之一。再考虑到提交都是有意义的——不是机器刷出来的，不是有意识的去刷，我觉得还是有很大成就感的。

而要实现500天连击很重要的两点是：时间和idea。但是我觉得idea并不是非常重要的，我们可以造轮子，这一点就是在早期我做得最多的一件事，不断地造轮子——如《[造轮子与从Github生成轮子](https://www.phodal.com/blog/create-framework-from-github/)》一文中所说。除此，你还可以用《[GitHub去管理你的idea](https://www.phodal.com/blog/use-github-manage-idea/)》，每当你想到一个Idea以及完成一个idea的时间你就会多一次提交。

时间则是一件很讽刺的事，因为人们要加班。加班的原因，要么是因为工作的内容很有意思，要么是因为钱。如果不是因为钱的话，为什么不去换个工作呢？比如我司。看似两者间存在很多的对立，但是我总在想技术的提升可以在后期解决收入的问题，而不需要靠加班来解决这个问题。人总是要活着的，钱是必需的，但是程序员的收入都不低。

### 编程的情绪周期

接着，我观察到了一些有意思的现象——编程的情绪周期也很明显。

> 所谓“情绪周期”，是指一个人的情绪高潮和低潮的交替过程所经历的时间。

如下图所示的就是情绪周期：

![情绪周期](./img/qingxu.jpg)

简单地来说，就是**有一个时间段写代码的感觉超级爽，有一个时间段不想写代码**，但是如果换一个说法就是：**有一个时间段看书、写文档的感觉很爽，有一时间段不想看书、写文档的感觉**。这也就是为什么在我的GitHub首页上的绿色各种花。不过因为《物联网周报》的原因，我会定期地更新一个相关的开源项目。

但是总来说，我习惯在一些时间造一些轮子、创建文档，这就是为什么我的GitHub会有一些开源电子书的缘故。

### 有意图的练习

编程需要很长的学习时间，也需要很长的练习时间。尽管我是从小学编程，自认为天赋不错，但是突破了上个门槛还是花费了三四年的时间。其中的很大一部分原因是，没有找对一个合适的方向。而在这期间也没有好好的练习，随后的日子里我意识到我会遇到下一个门槛，便开始试图有意识的练习。

在我开始工作的时候，我写了一篇名为《[重新思考工作](https://www.phodal.com/blog/rethink-about-the-work/)》的文章。在文章中我提到了几点练习的点：

 - 加强码代码的准确性
 - 写出更整洁的代码
 - 英语口语 （外企）
 - 针对性的加强语言技能

在一些日子的练习后，我发现这还是太无聊了。天生就喜欢一些有意思的东西，有趣才更有激情吧~~。不过，像下图的打字练习还是挺有意思的：

![打字练习](./img/huovd.png)

还是能打出了一堆错误的字符。但是对比了一下大多数人的人，还算不错，至少是盲打。但是，还是存在着很大的提升空间。

随后，我开始一些错误的练习，如对设计模式和架构的练习。试图去练习一些在生产上用不到的设计模式，以及一些架构模式。而这时就意味着，需要生搬一些设计模式。最后，我开始以项目为目的的练习，这就是为什么我的GitHub上的提交数会有如此多的原因。

### 预见性练习

还有一种练习比较有意思，算是以工作为导向的练习。当我们预见到我们的项目需要某一些技术，我们可能在未来采用某些技术的时候，我们就需要开始预见性的练习这些技术。

好的一点是：这些项目可能在未来很受初学者欢迎。

### 小结

每个人都有自己的方向，都有一个不错的发展路线，分享和创造都是不错的路。

THE ONLY FAIR IS NOT FAIR . ENJOY CREATE & SHARE.

## 365*2-7天里

刚毕业的时候，有一段时间我一直困惑于如何去提高编码能力——因为项目上做的东西多数时候和自己想要的是不一样的，我便想着自己去找一些有意思的东西做着玩，在这个过程中边练习技能。

> 如果你知道自己代码能力不够，为什么不花两年时间去提高这方面的能力呢？

### 编码的练习

编码是一件值得练习的事，你从书中、互联网上看到的那一个个的编程大牛无一不是从一点点的小技能积累起来的。从小接触可以让你有一个好的开始，一段好好的练习也会帮助你更好的前进。

记得我在最开始练习的时候，我分几个不同的阶段去练习：

 - 按照《重构：改善即有代码的设计》一书边寻找一些 bad smell 的代码，一边想方设法去让代码变得优雅。
 - 按照《设计模式》以及《重构与模式》来将代码重构成某种设计模式。
 - 按照《面向模式的软件架构》去设计一些软件架构。

而这些并不是一种容易的事，很多时候有一些模式，我们都很难有一个好的实践。只是这些东西都不是一些可以生搬硬套的，我们更需要的是知道有这些东西的存在，以便于在某一天，我们可以从我们的仓库里将这些知识取出来。

![10000 hours](./img/10000.png)

我们的刻意练习加上我们的持之以恒总是会取得长足的进步。不过在我们练习之前，你需要有一个目标。这个目标可以是一个 Idea、一个设计模式、一个模仿等等，这些内容都可以以 Issue 的好好管理着。

在最开始我们下定目标的几天里，我们可以很容易做到这样的事。同样的，我们也可以很容易达到 21 天。只是，我们很容易在 21 天后失去一些目标。所以在练习开始之前，你需要创建一个帮助你提高技术的列表，然后一点点加以提高。比如说：

1. 尝试使用 React + Redux + Koa 2、或者Angular 2 + TypeScript，这样我们就能凭此来学习新的技术。
2. 尝试使用 CQRS 架构来设计 CMS，这样我们就可以练习在架构方面的能力。

在我们想到一点我们可以练习的技术的时候，这就是一个可以变成 Issue 管理的内容，我们就可以针对性的提高。

通常在这种情况下，我们知道自己不知道什么东西，当我们处于不知道自己不知道、不知道自己知道时，那我们就需要网上的各种技能图谱——如StuQ的技能图谱。

![skilmap](./img/skillmap.png)

然后了解图谱上的一个个的内容，尽可能依照此构建自己的体系——以让自己走向知道自己不知道的地步，然后我们才依此来展开练习。

建议试试我们家的Growth哈，地址：http://growth.ren。

文章的剩下部分就让我分享一下：在这723天里，我创造出了哪些有意思的东西（ps：让我装逼一下）——其实我不仅仅只是 Markdown 写得好

#### 2014年

时间：2014.10.08-2014.12.30

![2014.png](./img/2014.png)

在这一段时间里，我创建的项目大部分都是一些物联网项目：

 - [iot-coap](https://github.com/phodal/iot-coap) 一个基于CoAP协议的物联网
 - [designiot](https://github.com/phodal/designiot) 即电子书《教你设计物联网系统》
 - [iot-document](https://github.com/phodal/awesome-iot-document) 收集一些物联网相关的资料，和Awesome不是一个性质
 - [iot](https://github.com/phodal/iot) 基于PHP框架Laravel的物联网
 - iot-android 一个与iot项目相配套的Android程序
 - 等等

正是这几个IoT项目，让Packt出版社找到了我，才有了后来和国内外出版社打交道的故事。也开始了技术审阅、翻译、写书的各种故事，想想就觉得这个开头真的很好。

期间还创建了一个很有意思的Chrome插件，叫onebuttonapp——没错，就是模仿Amazon的一键下单写的。这个插件的目的就是难证当时在项目上用的Backbone、Require.js的这一套可以在插件上好好玩。

OnMap项目是为了让我用Nokia Lumia 920拍照的照片，可以在地图上显示而创建的项目。

当然还有其他的一些小项目啦。

#### 2015年

![2015.png](./img/2015.png)

整个区间就是刷各种前端的技术栈，创建了各种有意思的项目：

 - [Lettuce框架](https://github.com/phodal/lettuce)，一个基于简单的SPA框架
 - [echoesworks](https://github.com/phodal/echoesworks)，一个支持字幕、Markdown、动画的Slide框架
 - [diaonan](https://github.com/phodal/diaonan)，一个支持CoAP、MQTT、HTTP的物联网项目
 - [developer](https://github.com/phodal/developer)，收集各种 Web Developer 成长路线，以及读书图谱

 
期间还创建了几个混合应用项目：
 
  - [learning-ionic](https://github.com/phodal/learning-ionic)，程序语言答人，各种hello,world的小应用
  - [ionic-elasticsearch](https://github.com/phodal/ionic-elasticsearch), Django ElasticSearch Ionic 打造 GIS 移动应用 
  - [designiot-app](https://github.com/phodal/designiot-app)，教你设计物联网APP版

更多内容可以见我的Idea列表：[https://github.com/phodal/ideas](https://github.com/phodal/ideas)，我实在是不想写了。

#### 2016年

![2016.png](./img/2016.png)

我们有了Growth系列的电子书、APP，还有Mole，几个极具代表性的项目就够了。

 - [Growth](https://github.com/phodal/growth)，一款专注于Web开发者成长的应用，涵盖Web开发的流程及技术栈，Web开发的学习路线、成长衡量等各方面。
 - [Growth：全栈增长工程师指南](https://github.com/phodal/growth-ebook)，一本关于如何成为全栈增长工程师的指南
 - [Growth：全栈增长工程师实战](https://github.com/phodal/growth-in-action)，在Growth中我们介绍的只是一系列的实践，而Growth实战则会带领读者去履行这些实践

### See you Again

停止这次连击，只是为了有一个更好的开始。

如果你也想提高自己，不妨从创建你的 ideas 项目开始，如我的[Ideas](https://github.com/phodal/ideas)项目一样，上面已经有了大量的 Idea。然后，我们还可以依据这一个个的项目，创建出一本电子书，即 [ideabook](https://github.com/phodal/ideabook)。

