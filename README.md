#GitHub 漫游指南

在线阅读: [GitHub 漫游指南](http://github.phodal.com/)， 下载: [pdf](https://github.com/phodal/github-roam/raw/gh-pages/github-roam.pdf)、[mobi](https://github.com/phodal/github-roam/raw/gh-pages/github-roam.mobi)、[epub](https://github.com/phodal/github-roam/raw/gh-pages/github-roam.epub)

关注我的微信公众号：

##简介

![qrcode](./img/qrcode.jpg)

2014年，写了《[一步步搭建物联网系统](https://github.com/phodal/designiot)》（电子书）。

2015.3.9号，想着写个《[GitHub漫游指南](http://github.phodal.com/)》，于是在最开始的地方写着：

> 我的GitHub主页上写着加入的时间——``Joined on Nov 8, 2010``，那时才大一，在那之后的那长日子里我都没有过到。也许是因为我学的不是计算机，到了今天——``2015.3.9``，我也发现这其实是程序员的社交网站。

但是过了很久都没有动静，今天是2015.10.24，我想是时候完成这个目标了。

##目录

<ul>
<li><a href="http://github.phodal.com/#前言">前言</a><ul>
<li><a href="http://github.phodal.com/#我与github的故事">我与GitHub的故事</a><ul>
<li><a href="http://github.phodal.com/#github与收获">GitHub与收获</a></li>
<li><a href="http://github.phodal.com/#github与成长">GitHub与成长</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#为什么你应该深入github">为什么你应该深入GitHub</a><ul>
<li><a href="http://github.phodal.com/#方便工作">方便工作</a></li>
<li><a href="http://github.phodal.com/#获得一份工作">获得一份工作</a></li>
<li><a href="http://github.phodal.com/#扩大交际">扩大交际</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#git基本知识与github使用">Git基本知识与GitHub使用</a><ul>
<li><a href="http://github.phodal.com/#git">Git</a><ul>
<li><a href="http://github.phodal.com/#git初入">Git初入</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#github">GitHub</a><ul>
<li><a href="http://github.phodal.com/#版本管理与软件部署">版本管理与软件部署</a></li>
<li><a href="http://github.phodal.com/#github与git">GitHub与Git</a></li>
<li><a href="http://github.phodal.com/#在github创建项目">在GitHub创建项目</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#github流行项目分析">GitHub流行项目分析</a></li>
<li><a href="http://github.phodal.com/#pull-request">Pull Request</a><ul>
<li><a href="http://github.phodal.com/#我的第一个pr">我的第一个PR</a></li>
<li><a href="http://github.phodal.com/#cla">CLA</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#构建github项目">构建GitHub项目</a><ul>
<li><a href="http://github.phodal.com/#如何用好github">如何用好GitHub</a><ul>
<li><a href="http://github.phodal.com/#敏捷软件开发">敏捷软件开发</a></li>
<li><a href="http://github.phodal.com/#测试">测试</a></li>
<li><a href="http://github.phodal.com/#ci">CI</a></li>
<li><a href="http://github.phodal.com/#代码质量">代码质量</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#模块分离与测试">模块分离与测试</a><ul>
<li><a href="http://github.phodal.com/#代码模块化">代码模块化</a></li>
<li><a href="http://github.phodal.com/#自动化测试">自动化测试</a></li>
<li><a href="http://github.phodal.com/#jshint">Jshint</a></li>
<li><a href="http://github.phodal.com/#mocha">Mocha</a></li>
<li><a href="http://github.phodal.com/#测试示例">测试示例</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#代码质量与重构">代码质量与重构</a><ul>
<li><a href="http://github.phodal.com/#code-climate">Code Climate</a></li>
<li><a href="http://github.phodal.com/#代码的坏味道">代码的坏味道</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#创建项目文档">创建项目文档</a><ul>
<li><a href="http://github.phodal.com/#readme">README</a></li>
<li><a href="http://github.phodal.com/#在线文档">在线文档</a></li>
<li><a href="http://github.phodal.com/#可用示例">可用示例</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#测试-1">测试</a><ul>
<li><a href="http://github.phodal.com/#tdd">TDD</a><ul>
<li><a href="http://github.phodal.com/#一次测试驱动开发">一次测试驱动开发</a></li>
<li><a href="http://github.phodal.com/#说说tdd">说说TDD</a></li>
<li><a href="http://github.phodal.com/#tdd思考">TDD思考</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#功能测试">功能测试</a><ul>
<li><a href="http://github.phodal.com/#轻量级网站测试twill">轻量级网站测试TWill</a></li>
<li><a href="http://github.phodal.com/#twill-登陆测试">Twill 登陆测试</a></li>
<li><a href="http://github.phodal.com/#twill-测试脚本">Twill 测试脚本</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#fake-server">Fake Server</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#重构">重构</a><ul>
<li><a href="http://github.phodal.com/#为什么重构">为什么重构?</a></li>
<li><a href="http://github.phodal.com/#重构umarkdown">重构uMarkdown</a><ul>
<li><a href="http://github.phodal.com/#代码说明">代码说明</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#interllij-idea重构">Interllij Idea重构</a><ul>
<li><a href="http://github.phodal.com/#rename">Rename</a></li>
<li><a href="http://github.phodal.com/#extract-method">Extract Method</a></li>
<li><a href="http://github.phodal.com/#inline-method">Inline Method</a></li>
<li><a href="http://github.phodal.com/#pull-members-up">Pull Members Up</a></li>
<li><a href="http://github.phodal.com/#重构之以查询取代临时变量">重构之以查询取代临时变量</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#如何在github寻找灵感fork">如何在GitHub“寻找灵感(fork)”</a><ul>
<li><a href="http://github.phodal.com/#lettuce构建过程"><a href="https://github.com/phodal/lettuce">Lettuce</a>构建过程</a><ul>
<li><a href="http://github.phodal.com/#需求">需求</a></li>
<li><a href="http://github.phodal.com/#计划">计划</a></li>
<li><a href="http://github.phodal.com/#实现第一个需求">实现第一个需求</a></li>
<li><a href="http://github.phodal.com/#实现第二个需求">实现第二个需求</a></li>
</ul></li>
</ul></li>
<li><a href="http://github.phodal.com/#github用户分析">GitHub用户分析</a><ul>
<li><a href="http://github.phodal.com/#生成图表">生成图表</a><ul>
<li><a href="http://github.phodal.com/#数据解析">数据解析</a></li>
<li><a href="http://github.phodal.com/#matplotlib">Matplotlib</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#每周分析">每周分析</a><ul>
<li><a href="http://github.phodal.com/#python-github-每周情况分析">python github 每周情况分析</a></li>
<li><a href="http://github.phodal.com/#python-数据分析">Python 数据分析</a></li>
<li><a href="http://github.phodal.com/#python-matplotlib图表">Python Matplotlib图表</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#存储到数据库中">存储到数据库中</a><ul>
<li><a href="http://github.phodal.com/#sqlite3">SQLite3</a></li>
<li><a href="http://github.phodal.com/#数据导入">数据导入</a></li>
<li><a href="http://github.phodal.com/#redis">Redis</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#邻近算法与相似用户">邻近算法与相似用户</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#github连击">GitHub连击</a><ul>
<li><a href="http://github.phodal.com/#天">100天</a><ul>
<li><a href="http://github.phodal.com/#天的提升">40天的提升</a></li>
<li><a href="http://github.phodal.com/#天的挑战">100天的挑战</a></li>
<li><a href="http://github.phodal.com/#天的希冀">140天的希冀</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#天的showcase">200天的Showcase</a><ul>
<li><a href="http://github.phodal.com/#一些项目简述">一些项目简述</a></li>
<li><a href="http://github.phodal.com/#google-map-solr-polygon-搜索">google map solr polygon 搜索</a></li>
<li><a href="http://github.phodal.com/#技能树">技能树</a></li>
</ul></li>
<li><a href="http://github.phodal.com/#天-1">365天</a><ul>
<li><a href="http://github.phodal.com/#编程的基础能力">编程的基础能力</a></li>
<li><a href="http://github.phodal.com/#技术与框架设计">技术与框架设计</a></li>
<li><a href="http://github.phodal.com/#领域与练习">领域与练习</a></li>
<li><a href="http://github.phodal.com/#其他-1">其他</a></li>
</ul></li>
</ul></li>
</ul>

更多请见[GitHub 漫游指南](http://github.phodal.com/)

## License

![cc](https://i.creativecommons.org/l/by-nc/4.0/88x31.png)

本作品采用[知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/)进行许可。

© 2015 [Phodal Huang](http://www.phodal.com)。[待我代码编成，娶你为妻可好](http://www.xuntayizhan.com/person/ji-ke-ai-qing-zhi-er-shi-dai-wo-dai-ma-bian-cheng-qu-ni-wei-qi-ke-hao-wan/)。

