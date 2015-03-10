#让我们连击

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
- 提了bug，并解决了。(ps:这是最理解的情况)

写在这本《Github 漫游指南》最后的地方，却是最开始写的希望的是有更多的人可以到这个同性交友网站。

##其他

把评论写在issue里作为你的第一个commit吧。

有兴趣一起漫游Github，QQ群:``322896123``
