#构建Github项目

##从模块分离到测试

在之前说到

> 奋斗了近半个月后，将fork的代码读懂、重构、升级版本、调整，添加新功能、添加测试、添加CI、添加分享之后，终于almost finish。

今天就来说说是怎样做的。

以之前造的[Lettuce](https://github.com/phodal/lettuce)为例，里面有:

 - 代码质量(Code Climate)
 - CI状态(Travis CI)
 - 测试覆盖率(96%)
 - 自动化测试(npm test)
 - 文档

按照[Web Developer路线图](https://github.com/phodal/awesome-developer)来说，我们还需要有:

 - 版本管理
 - 自动部署
 
等等。 

###Skillock模块化

在SkillTree的源码里，大致分为三部分:

 - namespace函数: 故名思意
 - Calculator也就是TalentTree，主要负责解析、生成url，头像，依赖等等
 - Skill 主要是tips部分。
 
而这一些都在一个js里，对于一个库来说，是一件好事，但是对于一个项目来说，并非如此。 

依赖的库有

 - jQuery
 - Knockout
 
好在Knockout可以用Require.js进行管理，于是，使用了``Require.js``进行管理:

```html
<script type="text/javascript" data-main="app/scripts/main.js" src="app/lib/require.js"></script>
```

``main.js``配置如下:

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
	
text、json插件主要是用于处理web.json，即用json来处理技能，于是不同的类到了不同的js文件。

	.
	|____Book.js
	|____Doc.js
	|____ko-bindings.js
	|____Link.js
	|____main.js
	|____Skill.js
	|____TalentTree.js
	|____Utils.js
	
加上了后来的推荐阅读书籍等等。而Book和Link都是继承自Doc。

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

而这里便是后面对其进行重构的内容。Doc类则是Skillock中类的一个缩影

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

或者说这是一个AMD的Class应该有的样子。考虑到this的隐性绑定，作者用了self=this来避免这个问题。最后Return了这个对象，我们在调用的就需要new一个。大部分在代码中返回的都是对象，除了在Utils类里面返回的是函数:

```javascript
return {
    getSkillsByHash: getSkillsByHash,
    getSkillById: getSkillById,				
    prettyJoin: prettyJoin
};
```
	
当然函数也是一个对象。	

###自动化测试

一直习惯用Travis CI，于是也继续用Travis Ci，``.travis.yml``配置如下所示:

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

使用gh-pages的原因是，我们一push代码的时候，就可以自动测试、部署等等，好处一堆堆的。

接着我们需要在``package.json``里面添加脚本

```javascript
"scripts": {
    "test": "mocha"
  }
```
	  
这样当我们push代码的时候便会自动跑所有的测试。因为mocha的主要配置是用``mocha.opts``，所以我们还需要配置一下``mocha.opts``

	--reporter spec
	--ui bdd
	--growl
	--colors
	test/spec	  

最后的``test/spec``是指定测试的目录。

###Jshint

> JSLint定义了一组编码约定，这比ECMA定义的语言更为严格。这些编码约定汲取了多年来的丰富编码经验，并以一条年代久远的编程原则 作为宗旨：能做并不意味着应该做。JSLint会对它认为有的编码实践加标志，另外还会指出哪些是明显的错误，从而促使你养成好的 JavaScript编码习惯。

当我们的js写得不合理的时候，这时测试就无法通过:

	line 5   col 25   A constructor name should start with an uppercase letter.
	line 21  col 62   Strings must use singlequote.
	
这是一种驱动写出更规范js的方法。


###Mocha

> Mocha 是一个优秀的JS测试框架，支持TDD/BDD，结合 should.js/expect/chai/better-assert，能轻松构建各种风格的测试用例。

最后的效果如下所示:

    Book,Link
      Book Test
        ✓ should return book label & url
      Link Test
        ✓ should return link label & url

###测试用例

简单地看一下Book的测试:

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

因为我们用``require.js``来管理浏览器端，在后台写测试来测试的时候，我们也需要用他来管理我们的依赖，这也就是为什么这个测试这么从的原因，多数情况下一个测试类似于这样子的。(用Jasmine似乎会是一个更好的主意，但是用习惯Jasmine了)

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

##Code Climate来clean code与重构

 - 当你写了一大堆代码,你没有意识到里面有一大堆重复。
 - 当你写了一大堆测试,却不知道覆盖率有多少。

这就是个问题了，于是偶然间看到了一个叫code climate的网站。

###Code Climate

> Code Climate consolidates the results from a suite of static analysis tools into a single, real-time report, giving your team the information it needs to identify hotspots, evaluate new approaches, and improve code quality.

Code Climate整合一组静态分析工具的结果到一个单一的，实时的报告，让您的团队需要识别热点，探讨新的方法，提高代码质量的信息。

简单地来说:

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

分享得到的最后的结果是:

![Coverage][1]

###代码的坏味道

于是我们就打开``lib/database/sqlite_helper.js``，因为其中有两个坏味道

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

 <hr>