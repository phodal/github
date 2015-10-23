#重构

或许你应该知道了，重构是怎样的，你也知道重构能带来什么。在我刚开始学重构和设计模式的时候，我需要去找一些好的示例，以便于我更好的学习。有时候不得不创造一些更好的场景，来实现这些功能。

有一天，我发现当我需要我一次又一次地重复讲述某些内容，于是我就计划着把这些应该掌握的技能放到Github上，也就有了[Artisan Stack](https://github.com/artisanstack) 计划。

每个程序员都不可避免地是一个Coder，一个没有掌握好技能的Coder，算不上是手工艺人，但是是手工人。

艺，需要有创造性的方法。

#[前端技能训练: 重构一](http://www.phodal.com/blog/frontend-improve-refactor-javascript-code/)

##为什么重构?

> 为了更好的代码。

在经历了一年多的工作之后，我平时的主要工作就是修Bug。刚开始的时候觉得无聊，后来才发现修Bug需要更好的技术。有时候你可能要面对着一坨一坨的代码，有时候你可能要花几天的时间去阅读代码。而，你重写那几十代码可能只会花上你不到一天的时间。但是如果你没办法理解当时为什么这么做，你的修改只会带来更多的bug。修Bug，更多的是维护代码。还是前人总结的那句话对:

> 写代码容易，读代码难。

假设我们写这些代码只要半天，而别人读起来要一天。为什么不试着用一天的时候去写这些代码，让别人花半天或者更少的时间来理解。

如果你的代码已经上线，虽然是一坨坨的。但是不要轻易尝试，``没有测试的重构``。

从前端开始的原因在于，写得一坨坨且最不容易测试的代码都在前端。

让我们来看看我们的第一个训练，相当有挑战性。

##重构uMarkdown

代码及setup请见github: [js-refactor](https://github.com/artisanstack/js-refactor)

###代码说明

``uMarkdown``是一个用于将Markdown转化为HTML的库。代码看上去就像一个很典型的过程代码:

```javascript
/* code */
while ((stra = micromarkdown.regexobject.code.exec(str)) !== null) {
  str = str.replace(stra[0], '<code>\n' + micromarkdown.htmlEncode(stra[1]).replace(/\n/gm, '<br/>').replace(/\ /gm, '&nbsp;') + '</code>\n');
}

/* headlines */
while ((stra = micromarkdown.regexobject.headline.exec(str)) !== null) {
  count = stra[1].length;
  str = str.replace(stra[0], '<h' + count + '>' + stra[2] + '</h' + count + '>' + '\n');
}

/* mail */
while ((stra = micromarkdown.regexobject.mail.exec(str)) !== null) {
  str = str.replace(stra[0], '<a href="mailto:' + stra[1] + '">' + stra[1] + '</a>');
}
```

选这个做重构的开始，不仅仅是因为之前在写[EchoesWorks](https://github.com/phodal/echoesworks)的时候进行了很多的重构。而且它更适合于，``重构到设计模式``的理论。让我们在重构完之后，给作者进行pull request吧。

Markdown的解析过程，有点类似于``Pipe and Filters``模式(架构模式)。

Filter即我们在代码中看到的正规表达式集:

```javascript
regexobject: {
    headline: /^(\#{1,6})([^\#\n]+)$/m,
    code: /\s\`\`\`\n?([^`]+)\`\`\`/g
```

他会匹配对应的Markdown类型，随后进行替换和处理。而``str```，就是管理口的输入和输出。

接着，我们就可以对其进行简单的重构。

###重构

(ps: 推荐用WebStrom来做重构，自带重构功能)

作为一个示例，我们先提出codeHandler方法，即将上面的

```javascript
/* code */
while ((stra = micromarkdown.regexobject.code.exec(str)) !== null) {
  str = str.replace(stra[0], '<code>\n' + micromarkdown.htmlEncode(stra[1]).replace(/\n/gm, '<br/>').replace(/\ /gm, '&nbsp;') + '</code>\n');
}
```
    
提取方法成

```javascript
codeFilter: function (str, stra) {
    return str.replace(stra[0], '<code>\n' + micromarkdown.htmlEncode(stra[1]).replace(/\n/gm, '<br/>').replace(/\ /gm, '&nbsp;') + '</code>\n');
  },    
```

while语句就成了

```javascript
while ((stra = regexobject.code.exec(str)) !== null) {
    str = this.codeFilter(str, stra);
}
```

然后，运行所有的测试。

```
grunt test
```

同理我们就可以``mail``、``headline``等方法进行重构。接着就会变成类似于下面的代码，

```javascript
/* code */
while ((execStr = regExpObject.code.exec(str)) !== null) {
str = codeHandler(str, execStr);
}

/* headlines */
while ((execStr = regExpObject.headline.exec(str)) !== null) {
str = headlineHandler(str, execStr);
}

/* lists */
while ((execStr = regExpObject.lists.exec(str)) !== null) {
str = listHandler(str, execStr);
}

/* tables */
while ((execStr = regExpObject.tables.exec(str)) !== null) {
str = tableHandler(str, execStr, strict);
}
```
	  
然后你也看到了，上面有一堆重复的代码，接着让我们用JavaScript的``奇技浮巧``，即apply方法，把上面的重复代码变成。

```javascript
['code', 'headline', 'lists', 'tables', 'links', 'mail', 'url', 'smlinks', 'hr'].forEach(function (type) {
    while ((stra = regexobject[type].exec(str)) !== null) {
        str = that[(type + 'Handler')].apply(that, [stra, str, strict]);
    }
});
```
		
进行测试，blabla，都是过的。

```javascript
 Markdown
   ✓ should parse h1~h3
   ✓ should parse link
   ✓ should special link
   ✓ should parse font style
   ✓ should parse code
   ✓ should parse ul list
   ✓ should parse ul table
   ✓ should return correctly class name
```
	   
快来试试吧， [https://github.com/artisanstack/js-refactor](https://github.com/artisanstack/js-refactor)