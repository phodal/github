#Github 100天

我也是蛮拼的，虽然我想的只是在Github上连击100~200天，然而到了今天也算不错。

![Longest Streak](../img/longest-streak.png)

``在停地造轮子的过程中，也不停地造车子。``

在那篇连续冲击365天的文章出现之前，我们公司的大大([https://github.com/dreamhead](https://github.com/dreamhead))也曾经在公司内部说过，天天commit什么的。当然这不是我的动力，在连击140天之前

- 给过google的``ngx_speed``、``node-coap``等项目创建过pull request
- 也有``free-programming-books``、``free-programming-books-zh_CN``这样的项目。
- 当然还有一个连击20天。

对比了一下365天连击的commit，我发现我在total上整整多了近0.5倍。

![365 Streak](../img/365-streak.jpg)

同时这似乎也意味着，我每天的commit数与之相比多了很多。

在连击20的时候，有这样的问题: *为了commit而commit代码*，最后就放弃了。

而现在是``为了填坑而commit``，为自己挖了太多的想法。


##40天的提升

当时我需要去印度接受毕业生培训，大概有5周左右，想着总不能空手而归。于是在国庆结束后有了第一次commit，当时旅游归来，想着自己在不同的地方有不同的照片，于是这个repo的名字是 [onmap](https://github.com/phodal/onmap)——将自己的照片显示在地图上的拍摄地点(手机是Lumia 920)。然而，中间因为修改账号的原因，丢失了commit。

再从印度说起，当时主要维护三个repo:

- 物联网的CoAP协议
- [一步步设计物联网系统](https://github.com/phodal/designiot)的电子书
- 一个Node.js + JS的网站

说说最后一个，最后一个是练习的项目。因为当时培训比较无聊，业余时间比较多，英语不好，加上听不懂印度人的话。晚上基本上是在住的地方默默地写代码，所以当时的目标有这么几个:

- TDD
- 测试覆盖率
- 代码整洁

这也就是为什么那个repo有这样的一行:

[![Build Status](https://api.travis-ci.org/phodal/freerice.png)](https://travis-ci.org/phodal/freerice)
[![Code Climate](https://codeclimate.com/github/phodal/freerice/badges/gpa.svg)](https://codeclimate.com/github/phodal/freerice)
[![Test Coverage](https://codeclimate.com/github/phodal/freerice/badges/coverage.svg)](https://codeclimate.com/github/phodal/freerice)
[![Dependencies](https://david-dm.org/phodal/freerice.svg?style=flat)](https://david-dm.org/phodal/freerice.svg?style=flat0)

做到98%的覆盖率也算蛮拼的，当然还有Code Climate也达到了4.0，也有了112个commits。因此也带来了一些提高:

- 提高了代码的质量(code climate比jslint更注重重复代码等等一些bad smell)。
- 对于Mock、Stub、FakesServer等用法有更好的掌握
- 可以持续地交付软件(版本管理、自动测试、CI、部署等等)

##100天的挑战

(ps:从印度回来之后，由于女朋友在泰国实习，有了更多的时间可以看书、写代码)

有意思的是越到中间的一些时间，commits的次数上去了，除了一些简单的pull request，还有一些新的轮子出现了。

![Problem](../img/problem.jpg)

这是上一星期的commits，这也就意味着，在一星期里面，我需要在8个repo里切换。而现在我又有了一个新的idea，这时就发现了一堆的问题:

 - 今天工作在这个repo上，突然发现那个repo上有issue，需要去修复，于是就放下了当前的代码。
 - 在不同的repo间切换容易分散精力
 - 很容易就发现有太多的功能可以实现，但是时间是有限的。
 - 没有足够的空闲时间，除了周末。
 - 希望去寻找那些有兴趣的人，然而却发现原来没有那么多时间去找人。

##140天的希冀

在经历了100天之后，似乎整个人都轻松了，毕竟目标是100~200天。似乎到现在，也不会有什么特殊的情怀，除了一些希冀。

当然，对于一个开源项目的作者来说，最好有下面的情况:

- 很多人知道了这个项目
- 很多人用它的项目。
- 在某些可以用这个项目快速解决问题的地方提到了这个项目
- 提了bug、issue、问题。
- 提了bug，并解决了。(ps:这是最理想的情况)


#Github 200天Showcase

今天是我连续泡在Github上的第200天，也是蛮高兴的，终于到达了:

![Github 200 days][1]

故事的背影是: 去年国庆完后要去印度接受毕业生培训——就是那个神奇的国度。但是在去之前已经在项目待了九个多月，项目上的挑战越来越少，在印度的时间又算是比较多。便给自己设定了一个长期的goal，即100~200天的longest streak。

或许之前你看到过一篇文章[让我们连击](https://github.com/phodal/github-roam/blob/master/chapters/12-streak-your-github.md)，那时已然140天，只是还是浑浑噩噩。到了今天，渐渐有了一个更清晰地思路。

先让我们来一下ShowCase，然后再然后，下一篇我们再继续。

##一些项目简述

上面说到的培训一开始是用Java写的一个网站，有自动测试、CI、CD等等。由于是内部组队培训，代码不能公开等等因素，加之做得无聊。顺手，拿Node.js +RESTify 做了Server，Backbone + RequireJS + jQuery 做了前台的逻辑。于是在那个日子里，也在维护一些旧的repo，如[iot-coap](https://github.com/phodal/iot-coap)、[iot](https://github.com/phodal/iot)，前者是我拿到WebStorm开源License的Repo，后者则是毕业设计。

对于这样一个项目也需要有测试、自动化测试、CI等等。CI用的是Travics-CI。总体的技术构架如下:

####技术栈

前台:

- Backbone 
- RequireJS
- Underscore
- Mustache
- Pure CSS

后台:

- RESTify

测试:

- Jasmine
- Chai
- Sinon
- Mocha
- Jasmine-jQuery

一直写到五星期的培训结束， 只是没有自动部署。想想就觉得可以用github-page的项目多好~~。

过程中还有一些有意思的小项目，如:

###google map solr polygon 搜索

[google map solr polygon 搜索](http://www.phodal.com/blog/google-map-width-solr-use-polygon-search/)

![google map solr][2]

代码: [https://github.com/phodal/gmap-solr](https://github.com/phodal/gmap-solr)

###技能树

这个可以从两部分说起:

#### 重构Skill Tree

原来的是

- Knockout
- RequireJS
- jQuery
- Gulp

![Skill Tree][3]

代码: [https://github.com/phodal/skillock](https://github.com/phodal/skillock)

####技能树Sherlock

- D3.js
- Dagre-D3.js
- jquery.tooltipster.js
- jQuery
- Lettuce
- Knockout.js
- Require.js

![Sherlock skill tree][4]

代码: [https://github.com/phodal/sherlock](https://github.com/phodal/sherlock)

###Django Ionic ElasticSearch 地图搜索

![Django Elastic Search][5]

- ElasticSearch
- Django
- Ionic
- OpenLayers 3

代码: [https://github.com/phodal/django-elasticsearch](https://github.com/phodal/django-elasticsearch)

###简历生成器

![Resume][6]

- React
- jsPDF
- jQuery
- RequireJS
- Showdown

代码: [https://github.com/phodal/resume](https://github.com/phodal/resume)


###Nginx 大数据学习

![Nginx Pig][7]

- ElasticSearch
- Hadoop
- Pig

代码: [https://github.com/phodal/learning-data/tree/master/nginx](https://github.com/phodal/learning-data/tree/master/nginx)

###其他

虽然技术栈上主要集中在Python、JavaScript，当然还有一些Ruby、Pig、Shell、Java的代码，只是我还是习惯用Python和JavaScript。一些用到觉得不错的框架:

- Ionic: 开始Hybird移动应用。
- Django: Python Web开发利器。
- Flask: Python Web开发小刀。
- RequireJS: 管理js依赖。
- Backbone: Model + View + Router。
- Angluar: ...。
- Knockout: MVV*。
- React: 据说会火。
- Cordova: Hybird应用基础。

还应该有:

- ElasticSearch
- Solr
- Hadoop
- Pig
- MongoDB
- Redis


  [1]: https://www.phodal.com/static/media/uploads/github-200-days.png
  [2]: https://www.phodal.com/static/media/uploads/screenshot.png
  [3]: https://www.phodal.com/static/media/uploads/skilltree.jpg
  [4]: https://www.phodal.com/static/media/uploads/screen_shot_2015-05-09_at_23.23.31.png
  [5]: https://www.phodal.com/static/media/uploads/elasticsearch_ionit_map.jpg
  [6]: https://www.phodal.com/static/media/uploads/resume.png
  [7]: https://www.phodal.com/static/media/uploads/nginx_pig.jpg
  
  #Github 365天
  
  给你一年的时间，你会怎样去提高你的水平？？？

![Github 365][13]

正值这难得的sick leave（万恶的空气），码文一篇来记念一个过去的366天里。尽管想的是在今年里写一个可持续的开源框架，但是到底这依赖于一个好的idea。在我的[Github 孵化器](http://github.com/phodal/ideas) 页面上似乎也没有一个特别让我满意的想法，虽然上面有各种不样有意思的ideas。多数都是在过去的一年是完成的，然而有一些也是还没有做到的。

##说说标题

尽管一直在Github上连击看上去似乎是没有多大必要的，但是人总得有点追求。如果正是漫无目的，却又想着提高技术的同时，为什么不去试试？毕竟技术非常好、不需要太多练习的人只是少数，似乎这样的人是不存在的。大多数的人都是经过练习之后，才会达到别人口中的“技术好”。

这让我想起了充斥着各种气味的知乎上的一些问题，在一些智商被完虐的话题里，无一不是因为那些人学得比别人早——哪来的天才？所谓的天才，应该是未来的智能生命一般，一出生什么都知道。如果并非如此，那只是说明他练习到位了。

练习不到位便意味着，即使你练习的时候是一万小时的两倍，那也是无济于事的。如果你学得比别人晚，在**很长的一段时间里**(可能直到进棺材)输给别人是必然的——落后就要挨打。就好像我等毕业于一所二本垫底的学校里，如果在过去我一直保持着和别人(各种重点)一样的学习速度，那么我只能一直是Loser。

需要注意的是，对你来说考上二本很难，并不是因为你比别人笨。教育资源分配不均的问题，在某种程度上导致了新的阶级制度的出现。如[我的首页](https://www.phodal.com/)说的那样: **THE ONLY FAIR IS NOT FAIR**——唯一公平的是它是不公平的。我们可以做的还有很多——**CREATE & SHARE**。真正的不幸是，因为营养不良导致的教育问题。

于是在想明白了很多事的时候起，便有了Re-Practise这样的计划，而365天只是中间的一个产物。

##编程的基础能力

虽说算法很重要，但是编码才是基础能力。算法与编程在某种程度上是不同的领域，算法编程是在编程上面的一级。算法写得再好，如果别人很难直接拿来复用，在别人眼里就是shit。想出能work的代码一件简单的事，学会对其重构，使之变得更易读就是一件有意义的事。

于是，在某一时刻在Github上创建了一个组织，叫[Artisan Stack](https://github.com/artisanstack)。当时想的是在Github寻找一些JavaScript项目，对其代码进行重构。但是到底是影响力不够哈，参与的人数比较少。

###重构

如果你懂得如何写出高可读的代码，那么我想你是不需要这个的，但是这意味着你花了更多的时候在思考上了。当谈论重构的时候，让我想起了TDD(测试驱动开发)。即使不是TDD，那么如果你写着测试，那也是可以重构的。(之前写过一些利用Intellij IDEA重构的文章：[提炼函数](https://www.phodal.com/blog/intellij-idea-refactor-extract-method/)、[以查询取代临时变量](https://www.phodal.com/blog/intellij-idea-refactor-replace-temp-with-query/)、[重构与Intellij Idea初探](https://www.phodal.com/blog/thoughtworks-refactor-and-intellij-idea/)、[内联函数](https://www.phodal.com/blog/intellij-idea-refactor-inline-method/))

在各种各样的文章里，我们看到过一些相关的内容，最好的参考莫过于《重构》一书。最基础不过的原则便是函数名，取名字很难，取别人能读懂的名字更难。其他的便有诸如长函数、过大的类、重复代码等等。在我有限的面试别人的经历里，这些问题都是最常见的。

###测试

而如果没有测试，其他都是扯淡。写好测试很难，写个测试算是一件容易的事。只是有些容易我们会为了测试而测试。

在我写[EchoesWorks](https://github.com/echoesworks/echoesworks)和[Lan](https://github.com/phodal/lan)的过程中，我尽量去保证足够高的测试覆盖率。

![lan][11] 

![EchoesWorks][14]

从测试开始的TDD，会保证方法是可测的。从功能到测试则可以提供工作次效率，但是只会让测试成为测试，而不是代码的一部分。

测试是代码的最后一公里。所以，尽可能的为你的Github上的项目添加测试。

###编码的过程

初到TW时，Pair时候总会有人教我如何开始编码，这应该也是一项基础的能力。结合日常，重新演绎一下这个过程：

1. 有一个可衡量、可实现、过程可测的目标
2. Tasking (即对要实现的目标过程进行分解)
3. 一步步实现 (如TDD)
4. 实现目标

放到当前的场景就是：

1. 我想在Github上连击365天。对应于每一个时候段的目标都应该是可以衡量、测试的——即每天都会有Contributions。
2. 分解就是一个痛苦的过程。理想情况下，我们应该会有每天提交，但是这取决于你的repo的数量，如果没有新的idea出现，那么这个就变成为了Contributions而Commit。
3. 一步步实现

在我们实际工作中也是如此，接到一个任务，然后分解，一步步完成。不过实现会稍微复杂一些，因为事务总会有抢占和优先级的。

##技术与框架设计

在上上一篇博客中《[After 500: 写了第500篇博客，然后呢?](https://www.phodal.com/blog/after-500-blogposts-analytics-after-tech/)》也深刻地讨论了下这个问题，技术向来都是后发者优势。对于技术人员来说，也是如此，后发者占据很大的优势。

如果我们只是单纯地把我们的关注点仅仅放置于技术上，那么我们就不具有任何的优势。而依赖于我们的编程经验，我们可以在特定的时候创造一些框架。而架构的设计本身就是一件有意思的事，大抵是因为程序员都喜欢创造。(ps:之前曾经写过这样一篇文章，《[对不起，我并不热爱编程，我只喜欢创造](https://www.phodal.com/blog/sorry-i-don't-like-programming/)》)

**创造是一种知识的再掌握过程。**

回顾一下写echoesworks的过程，一开始我需要的是一个网页版的PPT，当然这类的东西已经有很多了，如impress.js、bespoke.js等等。分析一下所需要的功能：markdown解析器、键盘事件处理、Ajax、进度条显示、图片处理、Slide。我们可以在Github上找到各式各样的模块，我们所要做的就是将之结合在一样。在那之前，我试着用类似的原理写（组合）了[Lettuce](https://github.com/phodal/lettuce)。

组合相比于创造过程是一个更有挑战性的过程，我们需要在这过程去设计胶水来粘合这些代码，并在最终可以让他工作。这好比是我们在平时接触到的任务划分，每个人负责相应的模块，最后整合。

想似的我在写[lan](https://github.com/phodal/lan)的时候，也是类似的，但是不同的是我已经设计了一个清晰的架构图。

![Lan IoT][12]

而在我们实现的编码过程也是如此，使用不同的框架，并且让他们能工作。如早期玩的[moqi.mobi](https://github.com/echoesworks/moqi.mobi)，基于Backbone、RequireJS、Underscore、Mustache、Pure CSS。在随后的时间里，用React替换了View层，就有了[backbone-react](https://github.com/phodal/backbone-react)的练习。

技术同人一样，需要不断地往高一级前进。我们只需要不断地Re-Practise。

##领域与练习 

说业务好像不太适合程序员的口味，那就领域吧。不同行业的人，如百度、阿里、腾讯，他们的领域核心是不一样的。

而领域本身也是相似的，这可以解释为什么互联网公司都喜欢互相挖人，而一般都不会去华为、中兴等非互联网领域挖人。出了这个领域，你可能连个毕业生都不如。领域、业务同技术一样是不断强化知识的一个过程。Ritchie先实现了BCPL语言，而后设计了C语言，而BCPL语言一开始是基于CPL语言。

领域本身也在不断进化。

这也是下一个值得提高的地方。

##其他

是时候写这个小结了。从不会写代码，到写代码是从0到1的过程，但是要从1到60都不是一件容易的事。无论是刷Github也好(不要是自动提交)，或者是换工作也好，我们都在不断地练习。

而练习是要分成不同的几个步骤，不仅仅局限于技术：

1. 编码
2. 架构
3. 设计
4. 。。。

  [11]: https://www.phodal.com/static/media/uploads/lan.png
  [12]: https://www.phodal.com/static/media/uploads/lan-iot.jpg
  [13]: https://www.phodal.com/static/media/uploads/github-365.jpg
  [14]: https://www.phodal.com/static/media/uploads/echoesworks.png
