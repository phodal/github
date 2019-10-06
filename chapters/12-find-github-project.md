如何在 GitHub "寻找灵感（fork）"
===

> 重造轮子是重新创造一个已有的或是已被其他人优化的基本方法。

最近萌发了一个想法写游戏引擎，之前想着做一个 JavaScript 前端框架。看看，这个思路是怎么来的。

## Lettuce 构建过程

> Lettuce 是一个简约的移动开发框架。

故事的出发点是这样的：``写了很多代码,用的都是框架，最后不知道收获什么了``？事实也是如此，当自己做了一些项目之后，发现最后什么也没有收获到。于是，就想着做一个框架。

### 需求

有这样的几个前提

 - 为什么我只需要 jQuery 里的选择器、Ajax 要引入那么重的库呢？
 - 为什么我只需要一个 Template，却想着用 Mustache
 - 为什么我需要一个 Router，却要用 Backbone 呢？
 - 为什么我需要的是一个 isObject 函数，却要用到整个 Underscore？

我想要的只是一个简单的功能，而我不想引入一个庞大的库。换句话说，我只需要不同库里面的一小部分功能，而不是一个库。

实际上想要的是：

> 构建一个库，里面从不同的库里面抽取出不同的函数。

### 计划

这时候我参考了一本电子书《Build JavaScript FrameWork》，加上一些平时的需求，于是很快的就知道自己需要什么样的功能：

 - Promise 支持
 - Class类（PS：没有一个好的类使用的方式）
 - Template 一个简单的模板引擎
 - Router 用来控制页面的路由 
 - Ajax 基本的 Ajax Get/Post 请求

在做一些实际的项目中，还遇到了这样的一些功能支持：

 - Effect 简单的一些页面效果
 - AMD 支持

而我们有一个前提是要保持这个库尽可能的小、同时我们还需要有测试。

### 实现第一个需求

简单说说是如何实现一个简单的需求。

#### 生成框架

因为 Yeoman 可以生成一个简单的轮廓，所以我们可以用它来生成这个项目的骨架。

 - Gulp
 - Jasmine

#### 寻找

在 GitHub 上搜索了一个看到了下面的几个结果：

- [https://github.com/then/promise](https://github.com/then/promise)
- [https://github.com/reactphp/promise](https://github.com/reactphp/promise)
- [https://github.com/kriskowal/q](https://github.com/kriskowal/q)
- [https://github.com/petkaantonov/bluebird](https://github.com/petkaantonov/bluebird)
- [https://github.com/cujojs/when](https://github.com/cujojs/when)

但是显然，他们都太重了。事实上，对于一个库来说，80% 的人只需要其中 20% 的代码。于是，找到了[https://github.com/stackp/promisejs](https://github.com/stackp/promisejs)，看了看用法，这就是我们需要的功能：

```javascript
function late(n) {
    var p = new promise.Promise();
    setTimeout(function() {
        p.done(null, n);
    }, n);
    return p;
}

late(100).then(
    function(err, n) {
        return late(n + 200);
    }
).then(
    function(err, n) {
        return late(n + 300);
    }
).then(
    function(err, n) {
        return late(n + 400);
    }
).then(
    function(err, n) {
        alert(n);
    }
);
```

接着打开看看 Promise 对象，有我们需要的功能，但是又有一些功能超出我的需求。接着把自己不需要的需求去掉，这里函数最后就变成了

```javascript
function Promise() {
    this._callbacks = [];
}

Promise.prototype.then = function(func, context) {
    var p;
    if (this._isdone) {
        p = func.apply(context, this.result);
    } else {
        p = new Promise();
        this._callbacks.push(function () {
            var res = func.apply(context, arguments);
            if (res && typeof res.then === 'function') {
                res.then(p.done, p);
            }
        });
    }
    return p;
};

Promise.prototype.done = function() {
    this.result = arguments;
    this._isdone = true;
    for (var i = 0; i < this._callbacks.length; i++) {
        this._callbacks[i].apply(null, arguments);
    }
    this._callbacks = [];
};

var promise = {
    Promise: Promise
};
```

需要注意的是：``License``，不同的软件有不同的 License，如 MIT、GPL 等等。最好能在遵循协议的情况下，使用别人的代码。

### 实现第二个需求

由于已经有了现有的很多库，所以就可以直接参照（抄）别人写的代码。

```javascript
Lettuce.get = function (url, callback) {
    Lettuce.send(url, 'GET', callback);
};

Lettuce.load = function (url, callback) {
    Lettuce.send(url, 'GET', callback);
};

Lettuce.post = function (url, data, callback) {
    Lettuce.send(url, 'POST', callback, data);
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
