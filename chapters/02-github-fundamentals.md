#Git基本知识与Github使用

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

###在Github创建项目

接着,我们试试在上面创建一个项目:

![Github Roam](./img/github-roam-create.jpg)

就会有下面的提醒:

![Github Roam](./img/project-init.jpg)

它提供多种方式的创建方法:

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

<hr />

##用好Github

如何用好Github,并实践一些敏捷软件开发是一个很有意思的事情.我们可以在上面做很多事情,从测试到CI,再到自动部署.

###敏捷软件开发

显然我是在扯淡，这和敏捷软件开发没有什么关系。不过我也不知道瀑布流是怎样的。说说我所知道的一个项目的组成吧:

 - 看板式管理应用程序(如trello，简单地说就是管理软件功能)
 - CI(持续集成)
 - 测试覆盖率
 - 代码质量(code smell)
 
对于一个不是远程的团队(如只有一个人的项目) 来说，Trello、Jenkin、Jira不是必需的:

> 你存在，我深深的脑海里

当只有一个人的时候，你只需要明确知道自己想要什么就够了。我们还需要的是CI、测试，以来提升代码的质量。

###测试

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

###CI

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

###代码质量

像``jslint``这类的工具，只能保证代码在语法上是正确的，但是不能保证你写了一堆bad smell的代码。

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

###重构

不想在这里说太多关于``重构``的东西，可以参考Martin Flower的《重构》一书去多了解一些重构的细节。

这时想说的是，只有代码被测试覆盖住了，那么才能保证重构的过程没有出错。

 <hr>