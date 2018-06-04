---
title: 使用Github和Hexo搭建博客
date: 2018-06-01 17:25:39
categories:
- tools
- blog
tags:
- Hexo
- GitHub
description: 使用github + hexo搭建博客，域名解析，配置插件
---

# 使用Github和Hexo搭建博客　
 
使用github + hexo搭建博客，域名解析，配置插件

## 前言
平时使用，主要用于记录自己的技术积累和重点知识。但由于自己太懒，能力也太渣，所以就一直没有行动。直到今年，突然发现随着知识积累的增加，有好多重要的内容脑袋都记不下了，有的网页就直接存个标签，但是标签越存越多，但却很少再次去浏览，最后知识还是会淡忘，所以今天痛下决心，还是自己搭个博客吧，以挽回知识的流失，同时也可以向外部分享自己的一些见解。

博客搭建过程也是一波三折，遇到各种坑爹问题，还好我没那么轻易放弃，最终在无数次失败之后终于成功了。

## 正文
### 1. github配置
1）首先需要有一个github账号，没有的话就得申请一个。
然后新建一个代码仓库，注意，仓库名一定要是：你的github账号名字.github.io，比如我的是guojunfei1993.github.io。
2）clone到本地，比如我的就是如下命令：
git clone https://github.com/guojunfei1993/guojunfei1993.github.io.git
cd 进文件夹，我们先建个index.html用于测试：
cd guojunfei1993.github.io
vim index.html
然后编辑：
```
<!DOCTYPE html>
<html>
<body>
<h1>github pages测试</h1>
</body>
</html>
```
然后按esc，再输入“:wq”回车保存。然后提交上去：
git add .
git commit -m “测试github pages”
git push
此时需要输入你的github账号和密码，输入就是了，成功后我们验证一下。
然后打开浏览器，输入地址，比如我的就是：http://guojunfei1993.github.io
如果能正确显示“github pages测试”字样，说明我们成功了。


### hexo安装
 Hexo 是一个简单地、轻量地、基于Node的一个静态博客框架。通过Hexo我们可以快速创建自己的博客，仅需要几条命令就可以完成。
安装hexo必须使用node.js环境，可以直接在[官网](https://hexo.io/zh-cn/index.html)下载编译完成的二进制代码或者在[github](https://github.com/nodejs/node)上下载源码包。
- 编译源码的过程中如果遇到g++版的问题，可以参考[这里](https://blog.csdn.net/gatieme/article/details/52871438)

接着安装hexo:
- 执行sudo npm install -g hexo
- 新建tmp文件夹，然后进入该文件夹
- 执行hexo init初始化hexo

完成之后测试一下：
- 输入hexo server控制台会打印:
```
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
```
- 然后通过浏览器打开地址：http://localhost:4000/

{% asset_img hexo.png This is an hexo image %}

打开了默认的网页界面



### 配置hexo
#### 设置资源文件夹，参考[网址](https://hexo.io/zh-cn/docs/asset-folders.html)
修改hexo根配置文件 _config.yml
```
_config.yml
post_asset_folder: true
```
当资源文件管理功能打开后，Hexo将会在你每一次通过 hexo new \[layout\] <\title\> 命令创建新文章时自动创建一个文件夹。这个资源文件夹将会有与这个 markdown 文件一样的名字。将所有与你的文章有关的资源放在这个关联文件夹中之后，你可以通过相对路径来引用它们，这样你就得到了一个更简单而且方便得多的工作流。

- 相对路径引用的标签插件

通过常规的 markdown 语法和相对路径来引用图片和其它资源可能会导致它们在存档页或者主页上显示不正确。在Hexo 2时代，社区创建了很多插件来解决这个问题。但是，随着Hexo 3 的发布，许多新的标签插件被加入到了核心代码中。这使得你可以更简单地在文章中引用你的资源。
```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```
比如说：当你打开文章资源文件夹功能后，你把一个 example.jpg 图片放在了你的资源文件夹中，如果通过使用相对路径的常规 markdown语法: 
```
![](/example.jpg) 
```
它将不会出现在首页上。（但是它会在文章中按你期待的方式工作）

- 正确的引用图片方式是使用下列的标签插件而不是 markdown ：
```
{% asset_img example.jpg This is an example image %}
```
通过这种方式，图片将会同时出现在文章和主页以及归档页中。

#### 设置皮肤，参考[网址](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/INSTALLATION.md):
```
cd guojunfei1993.github.io
git clone https://github.com/theme-next/hexo-theme-next themes/next
```
然后修改hexo根配置文件 _config.yml 中设置你的主题：
```
theme: next
```
#### 设置next主题，参考[网址](https://theme-next.iissnan.com/getting-started.html)

##### 主题设定

cheme 是 NexT 提供的一种特性，借助于 Scheme，NexT 为你提供多种不同的外观。同时，几乎所有的配置都可以 在 Scheme 之间共用。目前 NexT 支持三种 Scheme，他们是：
- Muse - 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
- Mist - Muse 的紧凑版本，整洁有序的单栏外观
- Pisces - 双栏 Scheme，小家碧玉似的清新
Scheme 的切换通过更改 主题配置文件，搜索 scheme 关键字。 你会看到有三行 scheme 的配置，将你需用启用的 scheme 前面注释 # 去除即可。
```
选择 Pisces Scheme
#scheme: Muse
#scheme: Mist
scheme: Pisces
```
##### 设置 语言
编辑 站点配置文件， 将 language 设置成你所需要的语言。建议明确设置你所需要的语言，例如选用简体中文，配置如下：
```
language: zh-Hans
```
目前 NexT 支持的语言如以下表格所示：


语言 |代码|设定示例
---|---|---
English	    |en	                |language: en
简体中文    |zh-Hans	        |language: zh-Hans
Français    |fr-FR	            |language: fr-FR
Português   |pt                 |language: pt or language: pt-BR
繁體中文    |zh-hk 或者 zh-tw   |language: zh-hk
Русский язык|ru	                |language: ru
Deutsch     |de	                |language: de
日本語      |ja	                |language: ja
Indonesian  |id	                |language: id
Korean      |ko                 |language: ko



---

### 新建博客
你可以执行下列命令来创建一篇新文章。
```
$ hexo new [layout] <title>
```
您可以在命令中指定文章的布局（layout），默认为 post，可以通过修改 _config.yml 中的 default_layout 参数来指定默认布局。

#### 布局（Layout）
Hexo 有三种默认布局：post、page 和 draft，它们分别对应不同的路径，而您自定义的其他布局和 post 相同，都将储存到 source/_posts 文件夹。

布局|	路径
---|---
post|	source/_posts
page|	source
draft|	source/_drafts


==不要处理我的文章==

如果你不想你的文章被处理，你可以将 Front-Matter 中的layout: 设为 false 。

#### 文件名称
Hexo 默认以标题做为文件名称，但您可编辑 new_post_name 参数来改变默认的文件名称，举例来说，设为 :year-:month-:day-:title.md 可让您更方便的通过日期来管理文章。

变量|	描述
---|---
:title|	标题（小写，空格将会被替换为短杠）
:year|	建立的年份，比如， 2015
:month|	建立的月份（有前导零），比如， 04
:i_month|	建立的月份（无前导零），比如， 4
:day	|建立的日期（有前导零），比如， 07
:i_day	|建立的日期（无前导零），比如， 7
#### 草稿
刚刚提到了 Hexo 的一种特殊布局：draft，这种布局在建立时会被保存到 source/_drafts 文件夹，您可通过 publish 命令将草稿移动到 source/_posts 文件夹，该命令的使用方式与 new 十分类似，您也可在命令中指定 layout 来指定布局。
```
$ hexo publish [layout] <title>
```
草稿默认不会显示在页面中，您可在执行时加上 --draft 参数，或是把 render_drafts 参数设为 true 来预览草稿。
#### 模版（Scaffold）
在新建文章时，Hexo 会根据 scaffolds 文件夹内相对应的文件来建立文件，例如：
```
$ hexo new photo "My Gallery"
```
在执行这行指令时，Hexo 会尝试在 scaffolds 文件夹中寻找 photo.md，并根据其内容建立文章，以下是您可以在模版中使用的变量：

变量|	描述
---|---
layout|	布局
title|	标题
date|	文件建立日期

### 发布到github

1. 将tmp文件夹下的所有文件移动到guojunfei1993.github.io文件夹下
2. 执行 npm install hexo-deployer-git --save ，安装发布工具
3. 输入静态化命令 ：hexo generate

    在本地目录下，会生成一个public的目录，里面包括了所有静态化的文件。

4. 打开_config.yml文件，设置github的项目地址：
```
deploy:
    type: git
    repo: https://github.com/guojunfei1993/guojunfei1993.github.io
#    branch: gh-pages
#    message: "Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }})"
```
5. 然后执行部署命令：hexo deploy
成功后验证，浏览器里输入地址：http://guojunfei1993.github.io

### HexoEditor
HexoEditor是一款为 Hexo 做了优化的 Markdown 编辑器。参考[网址](https://github.com/zhuzhuyule/HexoEditor/blob/master/doc/cn/README.md)
常用的快捷键设置如下：

按键	|方法	|说明
---|---|---
Tab	|tabAdd	|添加缩进
Shift - Tab	|tabSubtract	|减少缩进
Ctrl - B	|toggleBlod	|切换粗体
Ctrl - I	|toggleItalic	|切换斜体
Ctrl - D	|toggleDelete	|删除当前行
Ctrl - `	|toggleComment	|切换注解
Ctrl - L	|toggleUnOrderedList	|切换无序列表
Ctrl - Alt - L	|toggleOrderedList	|切换有序列表
Ctrl - ]	|toggleHeader	|降级标题
Ctrl - [	|toggleUnHeader	|升级标题
Ctrl - =	|toggleBlockquote	|增加引用
Ctrl - -	|toggleUnBlockquote	|减少引用
Ctrl - U	|drawLink	|添加超级链接
Ctrl - Alt - U	|drawImageLink	|添加图片
Ctrl - T	|drawTable(row col)	|添加表格(行 列)
Ctrl - V	|pasteOriginContent	|源内容粘贴
Shift - Ctrl - V	|pasteContent	|智能粘贴
Alt - F	|formatTables	|格式化表格
Ctrl - N	|	|新建md文档
Ctrl - H	|	|新建Hexo文档
Ctrl - O	|	|打开md文件
Ctrl - S	|	|保存文档
Shift - Ctrl - S	|	|另存为
Alt - Ctrl - S	|	|打开设置
Ctrl - W	|	|切换写作模式
Ctrl - P	|	|切换预览模式
Ctrl - R	|	|切换阅读模式
## 结语
第一次使用blog，学到了很多东西，感谢windrunnerlihuan博主，他的[文章](http://windrunnerlihuan.com/2016/05/27/%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E5%8E%86%E7%A8%8B/)给了很大帮助。
