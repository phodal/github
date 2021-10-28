# 介绍

## Github

Wiki百科上是这么说的

> GitHub 是一个共享虚拟主机服务，用于存放使用Git版本控制的软件代码和内容项目。它由GitHub公司（曾称Logical Awesome）的开发者Chris Wanstrath、PJ Hyett和Tom Preston-Werner
使用Ruby on Rails编写而成。

当然让我们看看官方的介绍:

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

jQuery[^jQuery]在发布版本``2.1.3``，一共有152个commit。我们可以看到如下的提交信息:

 - Ajax: Always use script injection in globalEval …	 bbdfbb4
 - Effects: Reintroduce use of requestAnimationFrame …	 72119e0
 - Effects: Improve raf logic …	 708764f
 - Build: Move test to appropriate module	 fbdbb6f
 - Build: Update commitplease dev dependency
 - ...

### Github与Git

> Git是一个分布式的版本控制系统，最初由Linus Torvalds编写，用作Linux内核代码的管理。在推出后，Git在其它项目中也取得了很大成功，尤其是在Ruby社区中。目前，包括Rubinius、Merb和Bitcoin在内的很多知名项目都使用了Git。Git同样可以被诸如Capistrano和Vlad the Deployer这样的部署工具所使用。

> GitHub可以托管各种git库，并提供一个web界面，但与其它像 SourceForge或Google Code这样的服务不同，GitHub的独特卖点在于从另外一个项目进行分支的简易性。为一个项目贡献代码非常简单：首先点击项目站点的“fork”的按钮，然后将代码检出并将修改加入到刚才分出的代码库中，最后通过内建的“pull request”机制向项目负责人申请代码合并。已经有人将GitHub称为代码玩家的MySpace。

[^jQuery]: jQuery是一套跨浏览器的JavaScript库，简化HTML与JavaScript之间的操作。

## 用好Github

如何用好Github,并实践一些敏捷软件开发是一个很有意思的事情.我们可以在上面做很多事情,从测试到CI,再到自动部署.

### 敏捷软件开发

显然我是在扯淡，这和敏捷软件开发没有什么关系。不过我也不知道瀑布流是怎样的。说说我所知道的一个项目的组成吧:

 - 看板式管理应用程序(如trello，简单地说就是管理软件功能)
 - CI(持续集成)
 - 测试覆盖率
 - 代码质量(code smell)
 
对于一个不是远程的团队(如只有一个人的项目) 来说，Trello、Jenkin、Jira不是必需的:

> 你存在，我深深的脑海里

当只有一个人的时候，你只需要明确知道自己想要什么就够了。我们还需要的是CI、测试，以来提升代码的质量。

### 测试

通常我们都会找Document，如果没有的话，你会找什么?看源代码，还是看测试?

```javascript
it("specifying response when you need it", function (done) {
	var doneFn = jasmine.createSpy("success");

	lettuce.get('/some/cool/url', function (result) {
		expect(result).toEqual("awesome response");
		done();
	});

	expect(jasmine.Ajax.requests.mostRecent().url).toBe('/some/cool/url');
	expect(doneFn).not.toHaveBeenCalled();

	jasmine.Ajax.requests.mostRecent().respondWith({
		"status": 200,
		"contentType": 'text/plain',
		"responseText": 'awesome response'
	});
});
```

代码来源: [https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

上面的测试用例，清清楚楚地写明了用法，虽然写得有点扯。

等等，测试是用来干什么的。那么，先说说我为什么会想去写测试吧:

 - 我不希望每次做完一个个新功能的时候，再手动地去测试一个个功能。(自动化测试)
 - 我不希望在重构的时候发现破坏了原来的功能，而我还一无所知。
 - 我不敢push代码，因为我没有把握。
 
虽然，我不是TDD的死忠，测试的目的是保证功能正常，TDD没法让我们写出质量更高的代码。但是有时TDD是不错的，可以让我们写出逻辑更简单地代码。

也许你已经知道了``Selenium``、``Jasmine``、``Cucumber``等等的框架，看到过类似于下面的测试

```
 Ajax
   ✓ specifying response when you need it
   ✓ specifying html when you need it
   ✓ should be post to some where
 Class
   ✓ respects instanceof
   ✓ inherits methods (also super)
   ✓ extend methods
 Effect
   ✓ should be able fadein elements
   ✓ should be able fadeout elements
```

代码来源: [https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)
	   
看上去似乎每个测试都很小，不过补完每一个测试之后我们就得到了测试覆盖率

File | Statements | Branches | Functions | Lines
-----|------------|----------|-----------|------
lettuce.js	| 98.58% (209 / 212)| 82.98%(78 / 94) | 100.00% (54 / 54) | 98.58% (209 / 212)

本地测试都通过了，于是我们添加了``Travis-CI``来跑我们的测试

### CI

虽然node.js不算是一门语言，但是因为我们用的node，下面的是一个简单的``.travis.yml``示例:

```yml
language: node_js
node_js:
	- "0.10"

notifications:
	email: false

before_install: npm install -g grunt-cli
install: npm install
after_success: CODECLIMATE_REPO_TOKEN=321480822fc37deb0de70a11931b4cb6a2a3cc411680e8f4569936ac8ffbb0ab codeclimate < coverage/lcov.info
```

代码来源: [https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

我们把这些集成到``README.md``之后，就有了之前那张图。

CI对于一个开发者在不同城市开发同一项目上来说是很重要的，这意味着当你添加的部分功能有测试覆盖的时候，项目代码会更加强壮。

### 代码质量

像``jslint``这类的工具，只能保证代码在语法上是正确的，但是不能保证你没有写一堆bad smell的代码。

 - 重复代码
 - 过长的函数
 - 等等
 
``Code Climate``是一个与github集成的工具，我们不仅仅可以看到测试覆盖率，还有代码质量。

先看看上面的ajax类:

```javascript
Lettuce.get = function (url, callback) {
	Lettuce.send(url, 'GET', callback);
};

Lettuce.send = function (url, method, callback, data) {
	data = data || null;
	var request = new XMLHttpRequest();
	if (callback instanceof Function) {
		request.onreadystatechange = function () {
			if (request.readyState === 4 && (request.status === 200 || request.status === 0)) {
				callback(request.responseText);
			}
		};
	}
	request.open(method, url, true);
	if (data instanceof Object) {
		data = JSON.stringify(data);
		request.setRequestHeader('Content-Type', 'application/json');
	}
	request.setRequestHeader('X-Requested-With', 'XMLHttpRequest');
	request.send(data);
};
```

代码来源: [https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

在[Code Climate](https://codeclimate.com/github/phodal/lettuce/src/ajax.js)在出现了一堆问题

 - Missing "use strict" statement. (Line 2)
 - Missing "use strict" statement. (Line 14)
 - 'Lettuce' is not defined. (Line 5)

而这些都是小问题啦，有时可能会有

 - Similar code found in two :expression_statement nodes (mass = 86)

这就意味着我们可以对上面的代码进行重构，他们是重复的代码。

### 重构

不想在这里说太多关于``重构``的东西，可以参考Martin Flower的《重构》一书去多了解一些重构的细节。

这时想说的是，只有代码被测试覆盖住了，那么才能保证重构的过程没有出错。
