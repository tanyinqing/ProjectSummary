 # 2017 08 17
>  [文档地址](https://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E6%9D%8E%E6%98%8E%E9%A3%9EJavaEE%E5%AD%A6%E4%B9%A0%2F%E6%96%87%E6%A1%A3%E5%9C%B0%E5%9D%80 "查看")→[源文件相关](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97%2FAndBaseDemo%E6%A1%86%E6%9E%B6 "查看")→[首页](https://tanyinqing.github.io/)→[老师文档](https://mingfei.gitbooks.io/java-big-data-engineer-training/content/)→[个人版文档](https://tanyinqing.gitbooks.io/java-big-data-engineer-training/content/)

<h1 id="1">目录1</h1> 

* 1HTML→[html讲义的理解](#0101)→[idea和快捷键](#0102)→[gitbook使用技巧](#0103)
* 2CSS→→[css讲义的理解](#0201)
* 3事件处理→[基于监听的事件处理](#0301)→[基于回调的事件处理](#0302)→[相应系统设置的事件和响应系统设置的更改](#0303)→[Handler消息传递机制](#0304)→[异步任务](#0305)


# 参考文档
 [老师讲义地址github](https://github.com/tanyinqing/Java-Big-Data-Engineer-Training "查看")
 [老师的软件地址](https://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E6%9D%8E%E6%98%8E%E9%A3%9EJavaEE%E5%AD%A6%E4%B9%A0%2F%E8%BD%AF%E4%BB%B6%E5%9C%B0%E5%9D%80 "查看")


<h1 id="0101">讲义的理解</h1>

[返回目录](#1) 

项目地址
[HTML_20170902](https://github.com/tanyinqing/HTML_20170902)

* [h5英文版学习网站](https://www.w3schools.com/html/default.asp)
* 里面介绍了很多html的知识，以及常用元素。
* [h5中文版翻译网站](http://w3school.com.cn/)
* [老师讲义](https://mingfei.gitbooks.io/java-big-data-engineer-training/content/)
* 
* [阿里云 最新活动 6个月的服务器免费](https://www.aliyun.com/)
* [老师的idea快捷键的地址](https://thu.github.io/IDEA/)
* [老师的代码仓库](https://github.com/thu)
* [chrome网上应用店](https://chrome.google.com/webstore/category/extensions?hl=zh-CN)
* [知乎网站](https://www.zhihu.com/)
* [俄罗斯搜索网站](https://yandex.com/)
* 
* [常用元素实现效果](https://github.com/tanyinqing/HTML_20170902/blob/master/img/index.jpg)→[常用元素源代码](https://github.com/tanyinqing/HTML_20170902/blob/master/index.html)
* [表单实现效果](https://github.com/tanyinqing/HTML_20170902/blob/master/img/form.jpg)→[表单源代码](https://github.com/tanyinqing/HTML_20170902/blob/master/forms.html)
* [其他实现效果](https://github.com/tanyinqing/HTML_20170902/blob/master/img/misc.jpg)→[其他源代码](https://github.com/tanyinqing/HTML_20170902/blob/master/misc.html)
* [markdown实现效果](https://github.com/tanyinqing/HTML_20170902/blob/master/img/markdown.jpg)→[markdown源代码](https://github.com/tanyinqing/HTML_20170902/blob/master/markdown.md)

网页上右键  检查 查看相关组件源代码
ctrl+P  把网页保存成PDF

github别人库中检出的的项目，如何上传到自己库中，右键show in Explorer找到原来的项目，删除原文件的.git文件夹，去掉项目的关联gitconfig就可以了。

.gitignore建立文件后，安装插件，有一些方便，可以有一些颜色提示，库名就变成了图标
```
.idea
LiMingFeiXiangMu.iml
```
chrome网上应用店  马克飞象  MarkDown的编辑器 支持所有的h5格式

add file to git?加入后就后在同步时，同步到库，不加入就不会同步。绿键表示新建，红色表示不加入。蓝色表示更改，灰色表示不会提交。也可以右键，git，加入。

把github的文件同步到gitbook
GitBook， your Profile， new ，github 
select a repository 
title的名字要一致

自己创建一个文件要有目录文件summary.md和readme.md文件，

如果新增加一个目录，就要在summary中增加节点，否则显示不出来。

gitbook下载PDF格式的文件，选中文件，settings，Features，选中E-Books

如果删除一本书，就输入全目录，例如tanyinqing/xiangmujingyan 

Gitbook关联Github，点Account settings，github，all的选项选中

Github：Your Gists，Create secret gist 保密文件
Create public gist 公开文件

库文件 setting transfer ownership 把自己的库分享给别人

Linus Torvalds Linus系统的创始人 git分布式系统的创始人 芬兰人 spring系统开源 server服务器使用的Linus系统

能够看明白别人写的代码，能学到不少东西。

gitbook中向github中同步文件，先在github中建立一I个相同名字的库，然后强制同步，按照gitbook同步，settings github，select a Repository,sync,点Force sync using GitBook content.

能分布控制的网站
国外的 能私有代码的
https://bitbucket.org/account/signup/
https://about.gitlab.com/
国内网站 会存在安全的问题
https://git.oschina.net/  码云网站

它们都是采用的git来上传的，git是一个软件，和github没有绑定的关系。

Yandex俄罗斯的搜索引擎

idea建立工程加上 /文件名

VPN 指的是翻墙软件，例如蓝灯，lantern软件。
VSCode 是一个写H5的软件，只是没有提示。
TeamViewer的会议模式，可以实现共享桌面。

 idea 建立文件的时候 加上斜线和项目名

idea 新建h5工程 static web  路径不要有中文名

利用idea建立一个网页。首先建立一个库，库的名字为  账号+.github.io,创建一个index.html 文件首页。并通过邮箱验证才可以。免费的个人页面


网页上 右键 检查：查看某一个控件的源码
查看网页源代码  查看全部的网站代码

idea输入法没有选字框：可能是百度输入法和它有冲突，卸载百度输入法，换上搜狗输入法就解决了。

逗号 分为英文半角 和中文全角

常用的浏览器
chrome google
firefox 火狐
IE 微软
opera
safari 苹果
yandex 俄罗斯
国内的浏览器内核还是ie
360 腾讯 uc

<h1 id="0102">idea和快捷键</h1>

[返回目录](#1) 

软件的注册 Intellij IDEA
```html
License_server_address
http://idea.iteblog.com/key.php
```
* shift+Num lk 开启和关闭数字小键盘
* ctrl+p 打印，可以把网页保存为PDF的格式
* ctrl+shift+k 再次提交
* ctrl+K 提交
* Alt+F2 浏览器展示
* Alt+1 左边目录的显示和隐藏
* tab 键 标记的快捷方式
* 鼠标选中工程 Alt+Insert 新建一个文件 HTML File文件
* File 文件为任意格式
* directory 建立一个路径 
* ctrl+D 复制一行
* ctrl+T 从网络更新项目
* ctrl+Alt+L 快速格式化

* table>tr>th*3 tab键  快速表格
* input:text 只有input与style的值组成 tab键才起作用

* shift+F6 改文件名
* 项目 右键 git revert 撤销多处改动

ctrl+shift+回车  为写样式的快捷键 

ctrl+w 增量选择
ctrl+shift+w 减量选择

ctrl+shift+加号和减号  全部折叠和展开
ctrl+加号和减号  个别方法折叠和展开

ctrl+x 删除一行
F2 定位问题的快捷键
Alt+回车 自动修复

<h1 id="0103">gitbook使用技巧</h1>

[返回目录](#1) 

1 写下一个目录是，一定看下目录结构是否正确；例如

 ```html
https://tanyinqing.gitbooks.io/projectsummary/content/html/intro/MingFeiMarkdown.html  如果目录重复，就不会出来
 ```
 一定在目录中注册的md文件，才能够被翻译成html文件，否则显示的是html格式的文件不正确。

<h1 id="0201">css讲义的理解</h1>

[返回目录](#1) 

1 github建立分支 上传后 点git master，New Branch建立一个新的分支，分支的名字是gh-pages,则按照
https://tanyinqing.github.io/css-zen-garden/  格式可以访问主页，按照
https://tanyinqing.github.io/css-zen-garden/tan  格式可以访问其他页面。这就相当于为单个项目又建立了一个页面。
单独复制到文件下的图片文件无法上传，必须选中，右键，git，add 加入git 才可以上传

如果更新主干代码，点local Branches，在点master origin/master(主干起源)，chechout,Smart Checkout智能选择。

[css英文学习网站  W3 School](http://www.w3schools.com/css/default.asp)
[css中文学习网站  W3 School](http://w3school.com.cn/css/index.asp)


项目地址
[CSS_20170902](https://github.com/tanyinqing/CSS_20170902)
项目页面
[页面](https://tanyinqing.github.io/CSS_20170902/)

 [css禅语花园 项目网页](http://csszengarden.com/)
[项目托管地址](https://github.com/mezzoblue/csszengarden.com)

Dave Shea 是他的作者

submit a design 提交一个新的样式方案

[google加载字体的网址](https://fonts.google.com/)

如何查看知乎网站的样式
查看源代码。搜css，点开，复制到.css文件中。格式化

样式花园模仿版作业
[个人版作业页面](https://tanyinqing.github.io/css-zen-garden/)

[官方样式解读](https://github.com/tanyinqing/css-zen-garden/blob/gh-pages/css/style_defeat.css)
[张文育首页](https://zhangwenyu2.github.io/css-zen-garden/)

<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/box-model.html">盒子模型</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/display.html">display</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/float.html">浮动float</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/font-family.html">字体的引入</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/intro.html">引入外部样式</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/jianshu.css">学习简书的样式</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/layout.html">运用div做一个布局</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/padding-border-margin.html">内外边界和边框</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/position.html">position</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/selector_1.html">颜色的取值范围</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/selector_5.html">属性选择器</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/selector_6.html">伪类的使用</a>
<a style="display: block" href="https://github.com/tanyinqing/CSS_20170902/blob/master/selector_7.html">伪元素的使用</a>






