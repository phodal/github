# 构建 GitHub 项目

## 如何用好 GitHub

如何用好 GitHub，并实践一些敏捷软件开发是一个很有意思的事情.我们可以在上面做很多事情,从测试到 CI,再到自动部署.

### 敏捷软件开发

显然我是在扯淡，这和敏捷软件开发没有什么关系。不过我也不知道瀑布流是怎样的。说说我所知道的一个项目的组成吧：

 - 看板式管理应用程序（如 trello，简单地说就是管理软件功能）
 - CI（持续集成）
 - 测试覆盖率
 - 代码质量（code smell）
 
对于一个不是远程的团队（如只有一个人的项目）来说，Trello、Jenkin、Jira不是必需的：

> 你存在，我深深的脑海里

当只有一个人的时候，你只需要明确知道自己想要什么就够了。我们还需要的是 CI、测试，以来提升代码的质量。

### 测试

通常我们都会找 Document，如果没有的话，你会找什么？看源代码，还是看测试？

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

代码来源：[https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

上面的测试用例，清清楚楚地写明了用法，虽然写得有点扯。

等等，测试是用来干什么的。那么，先说说我为什么会想去写测试吧：

 - 我不希望每次做完一个个新功能的时候，再手动地去测试一个个功能。（自动化测试）
 - 我不希望在重构的时候发现破坏了原来的功能，而我还一无所知。
 - 我不敢push代码，因为我没有把握。
 
虽然，我不是 TDD 的死忠，测试的目的是保证功能正常，TDD 没法让我们写出质量更高的代码。但是有时TDD是不错的，可以让我们写出逻辑更简单地代码。

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

代码来源：[https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)
	   
看上去似乎每个测试都很小，不过补完每一个测试之后我们就得到了测试覆盖率

File | Statements | Branches | Functions | Lines
-----|------------|----------|-----------|------
lettuce.js	| 98.58% (209 / 212)| 82.98%(78 / 94) | 100.00% (54 / 54) | 98.58% (209 / 212)

本地测试都通过了，于是我们添加了``Travis-CI``来跑我们的测试

### CI

虽然 node.js 不算是一门语言，但是因为我们用的 node，下面的是一个简单的 ``.travis.yml`` 示例：

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

代码来源：[https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

我们把这些集成到 ``README.md`` 之后，就有了之前那张图。

CI对于一个开发者在不同城市开发同一项目上来说是很重要的，这意味着当你添加的部分功能有测试覆盖的时候，项目代码会更加强壮。

### 代码质量

像 ``jslint`` 这类的工具，只能保证代码在语法上是正确的，但是不能保证你写了一堆 bad smell 的代码。

 - 重复代码
 - 过长的函数
 - 等等
 
``Code Climate`` 是一个与 GitHub 集成的工具，我们不仅仅可以看到测试覆盖率，还有代码质量。

先看看上面的 ajax 类：

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

代码来源：[https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

在 [Code Climate](https://codeclimate.com/github/phodal/lettuce/src/ajax.js) 在出现了一堆问题

 - Missing "use strict" statement. (Line 2)
 - Missing "use strict" statement. (Line 14)
 - 'Lettuce' is not defined. (Line 5)

而这些都是小问题啦，有时可能会有

 - Similar code found in two :expression_statement nodes (mass = 86)

这就意味着我们可以对上面的代码进行重构，他们是重复的代码。

## 模块分离与测试

在之前说到

> 奋斗了近半个月后，将 fork 的代码读懂、重构、升级版本、调整，添加新功能、添加测试、添加 CI、添加分享之后，终于 almost finish。

今天就来说说是怎样做的。

以之前造的 [Lettuce](https://github.com/phodal/lettuce) 为例，里面有：

 - 代码质量（Code Climate）
 - CI状态（Travis CI）
 - 测试覆盖率（96%）
 - 自动化测试（npm test）
 - 文档

按照 [Web Developer 路线图](https://github.com/phodal/awesome-developer)来说，我们还需要有：

 - 版本管理
 - 自动部署
 
等等。 

### 代码模块化

在 SkillTree 的源码里，大致分为三部分：

 - namespace 函数：顾名思义
 - Calculator 也就是 TalentTree，主要负责解析、生成 url，头像，依赖等等
 - Skill 主要是 tips 部分。
 
而这一些都在一个 JS 里，对于一个库来说，是一件好事，但是对于一个项目来说，并非如此。 

依赖的库有

 - jQuery
 - Knockout
 
好在 Knockout 可以用 Require.js 进行管理，于是，使用了 ``Require.js`` 进行管理：

```html
<script type="text/javascript" data-main="app/scripts/main.js" src="app/lib/require.js"></script>
```

``main.js`` 配置如下：

```javascript
require.config({
  baseUrl: 'app',
  paths:{
    jquery: 'lib/jquery',
    json: 'lib/json',
    text: 'lib/text'
  }
});

require(['scripts/ko-bindings']);

require(['lib/knockout', 'scripts/TalentTree', 'json!data/web.json'], function(ko, TalentTree, TalentData) {
  'use strict';
  var vm = new TalentTree(TalentData);
  ko.applyBindings(vm);
});
```
	
text、JSON 插件主要是用于处理 web.json，即用 JSON 来处理技能，于是不同的类到了不同的 JS 文件。

	.
	|____Book.js
	|____Doc.js
	|____ko-bindings.js
	|____Link.js
	|____main.js
	|____Skill.js
	|____TalentTree.js
	|____Utils.js
	
加上了后来的推荐阅读书籍等等。而 Book 和 Link 都是继承自 Doc。

```javascript
define(['scripts/Doc'], function(Doc) {
  'use strict';
  function Book(_e) {
    Doc.apply(this, arguments);
  }
  Book.prototype = new Doc();

  return Book;
});	
```

而这里便是后面对其进行重构的内容。Doc 类则是 Skillock 中类的一个缩影

```javascript
define([], function() {
  'use strict';
  var Doc = function (_e) {
    var e = _e || {};
    var self = this;

    self.label = e.label || (e.url || 'Learn more');
    self.url = e.url || 'javascript:void(0)';
  };

  return Doc;
});
```

或者说这是一个 AMD 的 Class 应该有的样子。考虑到 this 的隐性绑定，作者用了self=this 来避免这个问题。最后 Return 了这个对象，我们在调用的就需要 new 一个。大部分在代码中返回的都是对象，除了在 Utils 类里面返回的是函数：

```javascript
return {
    getSkillsByHash: getSkillsByHash,
    getSkillById: getSkillById,				
    prettyJoin: prettyJoin
};
```
	
当然函数也是一个对象。	

### 自动化测试

一直习惯用 Travis CI，于是也继续用 Travis Ci，``.travis.yml`` 配置如下所示：

```yml
language: node_js
node_js:
  - "0.10"

notifications:
  email: false

branches:
  only:
    - gh-pages
```

使用 gh-pages 的原因是，我们一 push 代码的时候，就可以自动测试、部署等等，好处一堆堆的。

接着我们需要在 ``package.json`` 里面添加脚本

```javascript
"scripts": {
    "test": "mocha"
  }
```
	  
这样当我们 push 代码的时候便会自动跑所有的测试。因为 mocha 的主要配置是用 ``mocha.opts``，所以我们还需要配置一下 ``mocha.opts``

	--reporter spec
	--ui bdd
	--growl
	--colors
	test/spec	  

最后的 ``test/spec`` 是指定测试的目录。

### JSLint

> JSLint定义了一组编码约定，这比ECMA定义的语言更为严格。这些编码约定汲取了多年来的丰富编码经验，并以一条年代久远的编程原则 作为宗旨：能做并不意味着应该做。JSLint会对它认为有的编码实践加标志，另外还会指出哪些是明显的错误，从而促使你养成好的 JavaScript编码习惯。

当我们的 JS 写得不合理的时候，这时测试就无法通过：

	line 5   col 25   A constructor name should start with an uppercase letter.
	line 21  col 62   Strings must use singlequote.
	
这是一种驱动写出更规范 JS 的方法。


### Mocha

> Mocha 是一个优秀的JS测试框架，支持TDD/BDD，结合 should.js/expect/chai/better-assert，能轻松构建各种风格的测试用例。

最后的效果如下所示：

    Book,Link
      Book Test
        ✓ should return book label & url
      Link Test
        ✓ should return link label & url

### 测试示例

简单地看一下 Book 的测试：

```javascript
/* global describe, it */

var requirejs = require("requirejs");
var assert = require("assert");
var should = require("should");
requirejs.config({
  baseUrl: 'app/',
  nodeRequire: require
});

describe('Book,Link', function () {
  var Book, Link;
  before(function (done) {
    requirejs(['scripts/Book'、], function (Book_Class) {
      Book = Book_Class;
      done();
    });
  });

  describe('Book Test', function () {
    it('should return book label & url', function () {
      var book_name = 'Head First HTML与CSS';
      var url = 'http://www.phodal.com';
      var books = {
        label: book_name,
        url: url
      };

      var _book = new Book(books);
      _book.label.should.equal(book_name);
      _book.url.should.equal(url);
    });
  });
});
```

因为我们用 ``require.js`` 来管理浏览器端，在后台写测试来测试的时候，我们也需要用他来管理我们的依赖，这也就是为什么这个测试这么长的原因，多数情况下一个测试类似于这样子的。（用 Jasmine 似乎会是一个更好的主意，但是用习惯 Jasmine 了）

```javascript
describe('Book Test', function () {
it('should return book label & url', function () {
  var book_name = 'Head First HTML与CSS';
  var url = 'http://www.phodal.com';
  var books = {
    label: book_name,
    url: url
  };

  var _book = new Book(books);
  _book.label.should.equal(book_name);
  _book.url.should.equal(url);
});
});
```

最后的断言，也算是测试的核心，保证测试是有用的。	  

## 代码质量与重构

 - 当你写了一大堆代码,你没有意识到里面有一大堆重复。
 - 当你写了一大堆测试,却不知道覆盖率有多少。

这就是个问题了，于是偶然间看到了一个叫 code climate 的网站。

### Code Climate

> Code Climate consolidates the results from a suite of static analysis tools into a single, real-time report, giving your team the information it needs to identify hotspots, evaluate new approaches, and improve code quality.

Code Climate 整合一组静态分析工具的结果到一个单一的，实时的报告，让您的团队需要识别热点，探讨新的方法，提高代码质量的信息。

简单地来说：

- 对我们的代码评分
- 找出代码中的坏味道

于是，我们先来了个例子

Rating	| Name |	Complexity |	Duplication	| Churn |	C/M	| Coverage |	Smells 
--------|------|--------------|-------------|----------|---------|---------------------
A |	lib/coap/coap_request_handler.js |	24 |	0 |	6 |	2.6 |	46.4% |	0
A |	lib/coap/coap_result_helper.js |	14	| 0	| 2 |	3.4 |	80.0% |	0
A	| lib/coap/coap_server.js |	16 |	0 |	5 |	5.2 |	44.0% |	0
A	| lib/database/db_factory.js |	8 |	0 |	3 |	3.8 |	92.3% |	0
A |	lib/database/iot_db.js |	7 |	0 |	6 |	1.0 |	58.8% |	0
A |	lib/database/mongodb_helper.js |	63 | 0 |	11 |	4.5	 | 35.0%	| 0
C |	lib/database/sqlite_helper.js |	32 |	86 |	10 |	4.5 |	35.0% |	2
B |	lib/rest/rest_helper.js	 | 19	| 62 |	3 |	4.7	| 37.5% |	2
A |	lib/rest/rest_server.js |	17 |	0 |	2 |	8.6	| 88.9% |	0
A |	lib/url_handler.js |	9 |	0	| 5 |	2.2	| 94.1% |	0

分享得到的最后的结果是：

![Coverage][1]

### 代码的坏味道

于是我们就打开 ``lib/database/sqlite_helper.js``，因为其中有两个坏味道

Similar code found in two :expression_statement nodes (mass = 86)

在代码的 ``lib/database/sqlite_helper.js:58…61 < >``

```javascript
    SQLiteHelper.prototype.deleteData = function (url, callback) {
        'use strict';
        var sql_command = "DELETE FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
        SQLiteHelper.prototype.basic(sql_command, callback);
```
        
lib/database/sqlite_helper.js:64…67 < >

与

```javascript
SQLiteHelper.prototype.getData = function (url, callback) {
    'use strict';
    var sql_command = "SELECT * FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    SQLiteHelper.prototype.basic(sql_command, callback);
```

只是这是之前修改过的重复。。

原来的代码是这样的

```javascript
SQLiteHelper.prototype.postData = function (block, callback) {
    'use strict';
    var db = new sqlite3.Database(config.db_name);
    var str = this.parseData(config.keys);
    var string = this.parseData(block);

    var sql_command = "insert or replace into " + config.table_name + " (" + str + ") VALUES (" + string + ");";
    db.all(sql_command, function (err) {
        SQLiteHelper.prototype.errorHandler(err);
        db.close();
        callback();
    });
};

SQLiteHelper.prototype.deleteData = function (url, callback) {
    'use strict';
    var db = new sqlite3.Database(config.db_name);
    var sql_command = "DELETE FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    db.all(sql_command, function (err) {
        SQLiteHelper.prototype.errorHandler(err);
        db.close();
        callback();
    });
};

SQLiteHelper.prototype.getData = function (url, callback) {
    'use strict';
    var db = new sqlite3.Database(config.db_name);
    var sql_command = "SELECT * FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    db.all(sql_command, function (err, rows) {
        SQLiteHelper.prototype.errorHandler(err);
        db.close();
        callback(JSON.stringify(rows));
    });
};
```
说的也是大量的重复，重构完的代码

```javascript
SQLiteHelper.prototype.basic = function(sql, db_callback){
    'use strict';
    var db = new sqlite3.Database(config.db_name);
    db.all(sql, function (err, rows) {
        SQLiteHelper.prototype.errorHandler(err);
        db.close();
        db_callback(JSON.stringify(rows));
    });

};

SQLiteHelper.prototype.postData = function (block, callback) {
    'use strict';
    var str = this.parseData(config.keys);
    var string = this.parseData(block);

    var sql_command = "insert or replace into " + config.table_name + " (" + str + ") VALUES (" + string + ");";
    SQLiteHelper.prototype.basic(sql_command, callback);
};

SQLiteHelper.prototype.deleteData = function (url, callback) {
    'use strict';
    var sql_command = "DELETE FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    SQLiteHelper.prototype.basic(sql_command, callback);
};

SQLiteHelper.prototype.getData = function (url, callback) {
    'use strict';
    var sql_command = "SELECT * FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    SQLiteHelper.prototype.basic(sql_command, callback);
};
```

重构完后的代码比原来还长，这似乎是个问题~~
