# 改善 GitHub 项目代码质量：测试

## TDD

虽然接触的 TDD 时间不算短，然而真正在实践 TDD 上的时候少之又少。除去怎么教人 TDD，就是与人结对编程时的 switch，或许是受限于当前的开发流程。

偶然间在开发一个物联网相关的开源项目——[Lan](https://github.com/phodal/lan)的时候，重拾了这个过程。不得不说提到的一点是，在我们的开发流程中**测试是由相关功能开发人员写的**，有时候测试是一种很具挑战性的工作。久而久之，为自己的开源项目写测试变成一种自然而然的事。有时没有测试，反而变得**没有安全感**。

### 一次测试驱动开发

之前正在重写一个[物联网](http://www.phodal.com/iot)的服务端，主要便是结合 CoAP、MQTT、HTTP 等协议构成一个物联网的云服务。现在，主要的任务是集中于协议与授权。由于，不同协议间的授权是不一样的，最开始的时候我先写了一个 http put 授权的功能，而在起先的时候是如何测试的呢？

    curl --user root:root -X PUT -d '{ "dream": 1 }' -H "Content-Type: application/json" http://localhost:8899/topics/test

我只要顺利在 request 中看有无 ``req.headers.authorization``，我便可以继续往下，接着给个判断。毕竟，我们对 HTTP 协议还是蛮清楚的。

```javascript
if (!req.headers.authorization) {
  res.statusCode = 401;
  res.setHeader('WWW-Authenticate', 'Basic realm="Secure Area"');
  return res.end('Unauthorized');
}
```       
       
可是除了 HTTP 协议，还有 MQTT 和 CoAP。对于 MQTT 协议来说，那还算好，毕竟自带授权，如：

```bash
mosquitto_pub -u root -P root -h localhost -d -t lettuce -m "Hello, MQTT. This is my first message."
```
       
便可以让我们简单地完成这个功能，然而有的协议是没有这样的功能如 CoAP 协议中是用 Option 来进行授权的。现在的工具如 libcoap 只能有如下的简单功能

```bash
coap-client -m get coap://127.0.0.1:5683/topics/zero -T
```

于是，先写了个测试脚本来验证功能。

```javascript
var coap     = require('coap');
var request  = coap.request;
var req = request({hostname: 'localhost',port:5683,pathname: '',method: 'POST'});

...

req.setHeader("Accept", "application/json");
req.setOption('Block2',  [new Buffer('phodal'), new Buffer('phodal')]);

...

req.end();
```
	
写完测试脚本后发现不对了，这个不应该是测试的代码吗？于是将其放到了 spec 中，接着发现了上面的全部功能的实现过程为什么不用 TDD 实现呢？

### 说说 TDD

测试驱动开发是一个很"古老"的程序开发方法，然而由于国内的开发流程的问题——即开发人员负责功能的测试，导致这么好的一项技术没有在国内推广。

测试驱动开发的主要过程是：

1. 先写功能的测试
2. 实现功能代码
3. 提交代码（commit -> 保证功能正常）
4. 重构功能代码

而对于这样的一个物联网项目来说，我已经有了几个有利的前提：

1. 已经有了原型
2. 框架设计

### TDD 思考

通常在我的理解下，TDD 是可有可无的。既然我知道了我要实现的大部分功能，而且我也知道如何实现。与此同时，对 Code Smell 也保持着警惕、要保证功能被测试覆盖。那么，总的来说 TDD 带来的价值并不大。

然而，在当前这种情况下，我知道我想要的功能，但是我并不理解其深层次的功能。我需要花费大量的时候来理解，它为什么是这样的，需要先有一些脚本来知道它是怎么工作的。TDD 变显得很有价值，换句话来说，在现有的情况下，TDD 对于我们不了解的一些事情，可以驱动出更多的开发。毕竟在我们完成测试脚本之后，我们也会发现这些测试脚本成为了代码的一部分。

在这种理想的情况下，我们为什么不 TDD 呢？


## 功能测试

### 轻量级网站测试 TWill

> twill was initially designed for testing Web sites, although since then people have also figured out that it's good for browsing unsuspecting Web sites.

之所以说轻量的原因是他是拿命令行测试的，还有 DSL，还有 Python。

除此之外，还可以拿它做压力测试，这种压力测试和一般的不一样。可以模拟整个过程，比如同时有多少人登陆你的网站。

不过，它有一个限制是没有 JavaScript。

看了一下源码，大概原理就是用 ``requests`` 下载 html，接着用 ``lxml`` 解析 html，比较有意思的是内嵌了一个 ``DSL``。

这是一个 Python 的库。

     pip install twill

### Twill 登陆测试

1.启动我们的应用。

2.进入 twill shell

    twill-sh
     -= Welcome to twill! =-
    current page:  *empty page*

3.打开网页

    >> go http://127.0.0.1:5000/login
    ==> at http://127.0.0.1:5000/login
    current page: http://127.0.0.1:5000/login

4.显示表单

    	>> showforms

	Form #1
	## ## __Name__________________ __Type___ __ID________ __Value__________________
	1     csrf_token               hidden    csrf_token   1423387196##5005bdf3496e09b8e2fbf450 ...
	2     email                    email     email        None
	3     password                 password  password     None
	4     login                    submit    (None)       登入

	current page: http://127.0.0.1:5000/login

5.填充表单

    formclear 1
    fv 1 email test@tes.com
    fv 1 password test

6.修改 action

    formaction 1 http://127.0.0.1:5000/login

7.提交表单

    >> submit
    Note: submit is using submit button: name="login", value="登入"
    current page: http://127.0.0.1:5000/

发现重定向到首页了。

### Twill 测试脚本

当然我们也可以用脚本直接来测试 ``login.twill``：

	go http://127.0.0.1:5000/login

	showforms
	formclear 1
	fv 1 email test@tes.com
	fv 1 password test
	formaction 1 http://127.0.0.1:5000/login
	submit

	go http://127.0.0.1:5000/logout

运行

     twill-sh login.twill

结果

	>> EXECUTING FILE login.twill
	AT LINE: login.twill:0
	==> at http://127.0.0.1:5000/login
	AT LINE: login.twill:2

	Form #1
	## ## __Name__________________ __Type___ __ID________ __Value__________________
	1     csrf_token               hidden    csrf_token   1423387345##7a000b612fef39aceab5ca54 ...
	2     email                    email     email        None
	3     password                 password  password     None
	4     login                    submit    (None)       登入

	AT LINE: login.twill:3
	AT LINE: login.twill:4
	AT LINE: login.twill:5
	AT LINE: login.twill:6
	Setting action for form  (<Element form at 0x10e7cbb50>,) to  ('http://127.0.0.1:5000/login',)
	AT LINE: login.twill:7
	Note: submit is using submit button: name="login", value="登入"

	AT LINE: login.twill:9
	==> at http://127.0.0.1:5000/login
	--
	1 of 1 files SUCCEEDED.

一个成功的测试诞生了。

## Fake Server

实践了一下怎么用 sinon 去 fake server，还没用 respondWith，于是写一下。

这里需要用到 sinon 框架来测试。

当我们 fetch 的时候，我们就可以返回我们想要 fake 的结果。

        var data = {"id":1,"name":"Rice","type":"Good","price":12,"quantity":1,"description":"Made in China"};
	beforeEach(function() {
		this.server = sinon.fakeServer.create();
		this.rices = new Rices();
		this.server.respondWith(
			"GET",
			"http://localhost:8080/all/rice",
			[
				200,
				{"Content-Type": "application/json"},
				JSON.stringify(data)
			]
		);
	});

于是在 afterEach 的时候，我们需要恢复这个 server。

	afterEach(function() {
		this.server.restore();
	});

接着写一个 jasmine 测试来测试

	describe("Collection Test", function() {
		it("should get data from the url", function() {
			this.rices.fetch();
			this.server.respond();
			var result = JSON.parse(JSON.stringify(this.rices.models[0]));
			expect(result["id"])
				.toEqual(1);
			expect(result["price"])
				.toEqual(12);
			expect(result)
				.toEqual(data);
		});
	});

