# 创建项目文档

我们需要为我们的项目创建一个文档，通常我们可以将核心代码以外的东西都称为文档：

1. README
2. 文档
3. 示例 
4. 测试

通常这个会在项目的最上方会有一个项目的简介，如下图所示：

![GitHub Project Introduction](./img/github-intro.png)

## README

README通常会显示在GitHub项目的下面，如下图所示：

![GitHub README](./img/readme-example.png)

通常一个好的README会让你立马对项目产生兴趣。

如下面的内容是React项目的简介：

![React README](./img/react-intro.png)

下面的内容写清楚了他们的用途：

* **Just the UI:** Lots of people use React as the V in MVC. Since React makes no assumptions about the rest of your technology stack, it's easy to try it out on a small feature in an existing project.
* **Virtual DOM:** React abstracts away the DOM from you, giving a simpler programming model and better performance. React can also render on the server using Node, and it can power native apps using [React Native](https://facebook.github.io/react-native/).
* **Data flow:** React implements one-way reactive data flow which reduces boilerplate and is easier to reason about than traditional data binding.

通常在这个README里，还会有：

* 针对人群
* 安装指南
* 示例
* 运行的平台
* 如何参与贡献
* 协议

## 官方首页与在线文档

很多开源项目都会有自己的网站，并在上面有一个文档，而有的则会放在[https://readthedocs.org/](https://readthedocs.org/)。

> Read the Docs 托管文档，让文档可以被全文搜索和更易查找。您可以导入您使用任何常用的版本控制系统管理的文档，包括 Mercurial、Git、Subversion 和 Bazaar。 我们支持 webhooks，因此可以在您提交代码时自动构建文档。并且同样也支持版本功能，因此您可以构建来自您代码仓库中某个标签或分支的文档。查看完整的功能列表 。

在一个开源项目中，良好和专业的文档是相当重要的，有时他可能会比软件还会重要。因为如果一个开源项目好用的话，多数人可能不会去查看软件的代码。这就意味着，多数时候他在和你的文档打交道。文档一般会有：API 文档、 配置文档、帮助文档、用户手册、教程等等

写文档的软件有很多，如Markdown、Doxygen、Docbook等等。

## 可用示例

一个简单上手的示例非常重要，特别是通常我们是在为着某个目的而去使用一个开源项目的是时候，我们希望能马上使用到我们的项目中。

你希望看到的是，你打开浏览器，输入下面的代码，然后**It Works**：

```
var HelloMessage = React.createClass({
  render: function() {
    return <div>Hello {this.props.name}</div>;
  }
});

React.render(
  <HelloMessage name="John" />,
  document.getElementById('container')
);
```

而不是需要繁琐的步骤才能进行下一步。
