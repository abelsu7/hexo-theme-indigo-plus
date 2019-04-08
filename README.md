# hexo-theme-indigo-plus

> 基于 [hexo-theme-indigo](https://github.com/yscoder/hexo-theme-indigo) 优化，更新中...

## Feature

* 添加**直达评论悬浮按钮**
* **归档、分类、标签页面**添加**文章计数**
* 修改打赏的**切换按钮样式**
* 优化 **Valine** 在 hexo-theme-indigo 中的**显示效果**
* 优化 **hexo-douban** 在 hexo-theme-indigo 中的**显示效果**
* 使用 **prism.js** 替换 highlight.js 实现**代码高亮**，并在`_config.yml`中添加代码主题配置项
* 可控制**仅在单个 post 中引入**`MathJax.js`

> hexo-douban 同样做了相应修改，之后会补充说明

* Change ul list-style and toc bottom padding
* 更新 busuanzi CDN 地址
* `tags`及`categories`页面按照**字母顺序**排序
* 文章置顶
* 敬请期待...

## 快速开始

### 1. 安装 Hexo

```bash
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```

### 2. 设置语言并禁用 highlight.js

修改**博客根目录**下的`_config.yml`，设置`language`为`zh-CN`，并将`highlight`设置为`false`：

```yaml
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: Keep Coding
subtitle: 苏易北
description: Abel Su的编程笔记
author: Abel Su
language: zh-CN
timezone:
...
...
highlight:
  enable: false
  # line_number: true
  # auto_detect: false
  # tab_replace: 
...
...
```

### 3. 主题安装

安装需确认你的 **Hexo** 版本在`3.0`以上，以及 **Node** 版本为`6.x`以上，在**博客根目录**，执行以下命令：

```bash
git clone https://github.com/abelsu7/hexo-theme-indigo-plus.git themes/indigo-plus
```

之后在**博客根目录**下的`_config.yml`中指定使用主题`indigo-plus`：

```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: indigo-plus
```

### 4. 依赖安装

还是在**博客根目录**下，如果以下插件已安装过，则无需再次安装。

#### Less

主题默认使用`less`作为`css`预处理工具：

```bash
npm install hexo-renderer-less --save
```

#### Feed

用于生成`rss`：

```bash
npm install hexo-generator-feed --save
```

#### JSON-Content

用于生成静态站点数据，用作**站内搜索**的数据源：

```bash
npm install hexo-generator-json-content --save
```

#### QR-Code

> **可选**，不安装时会请求`jiathis API`生成二维码

用于生成微信分享二维码：

```bash
npm install hexo-helper-qrcode --save
```

#### Deploy

可以使用`hexo deploy`命令**部署博客**：

```bash
npm install hexo-deployer-git --save
```

#### Kramed

使用`hexo-renderer-kramed`替换默认的`hexo-renderer-marked`渲染引擎，否则使用`prism.js`高亮代码时会出现问题：

```bash
npm uninstall hexo-renderer-marked --save
npm install hexo-renderer-kramed --save
```

#### Douban

首先安装`hexo-douban`：

```bash
npm install hexo-douban --save
```

之后在**博客根目录**下的`_config.yml`中添加如下配置（以下为示例，请根据需要自行修改）：

```yaml
# hexo-douban config
douban:
  user: abelsu7 # your Douban ID
  builtin: false
  book: 
    title: '读书'
    quote: <p>注：<b><font color="#3f51b5">IE、Edge及Safari</font></b>中无法正常加载图片<br/>请移步我的<a href="https://book.douban.com/people/abelsu7/" target="_blank"><font color="#ff4081">豆瓣读书</font></a>主页</p>
    subtitle: 'Books are the ladder of human progress.'
  movie:
    title: '影视'
    quote: <p>注：<b><font color="#3f51b5">IE、Edge及Safari</font></b>中无法正常加载图片<br/>请移步我的<a href="https://movie.douban.com/people/abelsu7/" target="_blank"><font color="#ff4081">豆瓣电影</font></a>主页</p>
    subtitle: '如果有多一张船票，你会不会跟我一起走？'
  game:
    title: '游戏'
    quote: <p>注：<b><font color="#3f51b5">IE、Edge及Safari</font></b>中无法正常加载图片<br/>请移步我的<a href="https://www.douban.com/people/abelsu7/games?action=collect" target="_blank"><font color="#ff4081">豆瓣游戏</font></a>主页</p>
    subtitle: '胜败乃兵家常事，大侠请重新来过'
  timeout: 40000
```

此时运行`hexo-douban`已经可以生成相应的页面。但为使其风格与本主题更加协调，还需手动修改`hexo-douban`插件的部分代码。

首先进入`node_modules/hexo-douban/lib/templates`目录，分别将`book.ejs`、`movie.ejs`、`game.ejs`替换为以下内容。

`book.ejs`内容如下：

```js
<blockquote>
    <p>
        <%- quote; %>
    </p>
</blockquote>

<style>
    <% include index.css %>
</style>

<div class="container body-wrap card">
    <article class="page-article fade" itemprop="blogPage">

        <div class="hexo-douban-tabs">
            <a class="hexo-douban-tab" id="hexo-douban-tab1" href="javascript:;" rel="external">
                <%= __('bookReading') %>
                (
                <%= reading.length %>)</a>
            <a class="hexo-douban-tab" id="hexo-douban-tab2" href="javascript:;" rel="external">
                <%= __('bookWish') %>
                (
                <%= wish.length %>)</a>
            <a class="hexo-douban-tab" id="hexo-douban-tab3" href="javascript:;" rel="external">
                <%= __('bookRead') %>
                (
                <%= read.length %>)</a>
        </div>
        <div>
            <div id="hexo-douban-item1">
                <% reading.forEach(function(item){ %>
                <% include bookReading.ejs %>
                <% }); %>
                <% include pagination.ejs %>
            </div>
            <div id="hexo-douban-item2">
                <% wish.forEach(function(item){ %>
                <% include bookWish.ejs %>
                <% }); %>
                <% include pagination.ejs %>

            </div>
            <div id="hexo-douban-item3">
                <% read.forEach(function(item){ %>
                <% include bookRead.ejs %>
                <% }); %>
                <% include pagination.ejs %>
            </div>

        </div>

    </article>
</div>

<script>
    <% include index.js %>
    <% include pagination.js %>
</script>
```

`movie.ejs`内容如下：

```js
<blockquote>
    <p>
        <%- quote; %>
    </p>
</blockquote>

<style>
    <% include index.css %>
</style>

<div class="container body-wrap card">
    <article class="page-article fade" itemprop="blogPage">

        <div class="hexo-douban-tabs">
            <a class="hexo-douban-tab" id="hexo-douban-tab1" href="javascript:;" rel="external">
                <%= __('movieWatching') %>
                (
                <%= watching.length %>)</a>
            <a class="hexo-douban-tab" id="hexo-douban-tab2" href="javascript:;" rel="external">
                <%= __('movieWish') %>
                (
                <%= wish.length %>)</a>
            <a class="hexo-douban-tab" id="hexo-douban-tab3" href="javascript:;" rel="external">
                <%= __('movieWatched') %>
                (
                <%= watched.length %>)</a>
        </div>
        <div>
            <div id="hexo-douban-item1">
                <% watching.forEach(function(item){ %>
                <% include movieWatching.ejs %>
                <% }); %>
                <% include pagination.ejs %>
            </div>
            <div id="hexo-douban-item2">
                <% wish.forEach(function(item){ %>
                <% include movieWish.ejs %>
                <% }); %>
                <% include pagination.ejs %>
            </div>
            <div id="hexo-douban-item3">
                <% watched.forEach(function(item){ %>
                <% include movieWatched.ejs %>
                <% }); %>
                <% include pagination.ejs %>
            </div>
        </div>

    </article>
</div>

<script>
    <% include index.js %>
    <% include pagination.js %>
</script>
```

`game.ejs`内容如下：

```js
<blockquote>
    <p>
        <%- quote %>
    </p>
</blockquote>

<style>
    <% include index.css %>
</style>

<div class="container body-wrap card">
    <article class="page-article fade" itemprop="blogPage">

        <div class="hexo-douban-tabs">
            <a class="hexo-douban-tab" id="hexo-douban-tab1" href="javascript:;" rel="external">
                <%= __('gamePlaying') %>
                (
                <%= playing.length %>)</a>
            <a class="hexo-douban-tab" id="hexo-douban-tab2" href="javascript:;" rel="external">
                <%= __('gameWish') %>
                (
                <%= wish.length %>)</a>
            <a class="hexo-douban-tab" id="hexo-douban-tab3" href="javascript:;" rel="external">
                <%= __('gamePlayed') %>
                (
                <%= played.length %>)</a>

        </div>
        <div>
            <div id="hexo-douban-item1">
                <% playing.forEach(function(item){ %>
                <% include gamePlaying.ejs %>
                <% }); %>
                <% include pagination.ejs %>
            </div>
            <div id="hexo-douban-item2">
                <% wish.forEach(function(item){ %>
                <% include gameWish.ejs %>
                <% }); %>
                <% include pagination.ejs %>
            </div>
            <div id="hexo-douban-item3">
                <% played.forEach(function(item){ %>
                <% include gamePlayed.ejs %>
                <% }); %>
                <% include pagination.ejs %>
            </div>

        </div>

    </article>
</div>

<script>
    <% include index.js %>
    <% include pagination.js %>
</script>
```

之后打开该目录下的`index.css`，添加或修改以下样式：

```css
.hexo-douban-tabs {
    margin-bottom: 15px;
    margin-top: 15px;
    text-align: center; /* 新增  */
}

.hexo-douban-tab {
    color: #303f9f; /* 新增 */
    padding: 5px;
}

/* 新增 .hexo-douban-tab:hover */
.hexo-douban-tab:hover {
    color: #ff4081;
}

/* 修改 .hexo-douban-active */
.hexo-douban-active {
    /* background: #657b83; */
    /* color: #fff; */
    color: #ff4081;
}
...
...
/* 修改 .hexo-douban-button:hover */
.hexo-douban-button:hover {
    /* background: #657b83; */
    /* color: #fff; */
    color: #ff4081;
}
...
...
```

最后在`books-generator.js`、`movies-generator.js`、`games-generator.js`最后的`return`语句中，添加对应的`layout`：

`books-generator.js`的最后：

```js
...
...
    return {
        path: 'books/index.html',
        data: {
            title: config.douban.book.title,
            content: contents,
            slug: 'books'
        },
        layout: ['book', 'page', 'post'] // 添加 'book'
    };
};
```

`movies-generator.js`的最后：

```js
...
...
    return {
        path: 'movies/index.html',
        data: {
            title: config.douban.movie.title,
            content: contents,
            slug: 'movies'
        },
        layout: ['movie', 'page', 'post'] // 添加 'movie'
    };
};
```

`games-generator.js`的最后：

```js
...
...
    return {
        path: 'games/index.html',
        data: {
            title: config.douban.game.title,
            content: contents,
            slug: 'games'
        },
        layout: ['game', 'page', 'post'] // 添加 'game'
    };
};
```

### 5. 修改 scaffolds

初始化 Hexo 博客后，默认会在`scaffolds`目录下创建`draft.md`、`page.md`、`post.md`三个模板文件，使用`hexo new`命令新建页面时就会基于上述模板文件生成对应的 Markdown 文件。为了方便使用，建议将`scaffolds`下的模板文件修改如下：

`draft.md`：

```yaml
---
title: {{ title }}
category:
  - 
tags:
  - 
date: {{ date }}
top: 1
---
```

`page.md`：

```yaml
---
layout: page
title: {{ title }}
date: {{ date }}
top: 1
---
```

`post.md`：

```yaml
---
title: {{ title }}
category:
  - 
tags:
  - 
date: {{ date }}
top: 1
---
```

这里添加了`top: 1`属性，是为了实现文章置顶功能，参见 [Hexo 实现自定义文章置顶 | 苏易北](https://abelsu7.top/2019/02/28/hexo-pin-top/)。


### 6. 文章置顶

修改博客根目录下`_config.yml`文件：

```yaml
...
...
# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 10
  order_by: 
    top: -1
    date: -1
...
...
```

即可在首页先根据`top`值、再根据`date`，对所有文章进行排序。所有文章默认`top: 1`，如需置顶文章，只需将其`top`值修改为大于 1 的整数，同一`top`值可有多篇文章，`top`值相同时按照`date`排序。

> 注意：需要确保所有的`post`都有`top`和`date`属性，否则会导致排序失败。可在每次新建文章时使用`hexo new post 'title'`创建，即可根据`post.md`模板生成对应的文章文件

### 7. 按需开启 MathJax

可以按需开启`MathJax`支持。首先确保`themes/indigo-plus/_config.yml`中，`mathjax`设置为`true`：

```yaml
...
...
# 文章截断
excerpt_render: true
excerpt_length: 200
excerpt_link: 阅读全文...
mathjax: true
archive_yearly: true
...
...
```

如要在某篇文章中开启`MathJax`支持，只需在其`YAML`头部中加入`mathjax: true`，例如：

```yaml
---
title: 在 Hexo 中使用 MathJax 渲染数学公式
category:
  - 前端
tags:
  - Hexo
  - MathJax
  - LaTex
  - 数学
date: 2018-10-29 19:58:35
top: 1
mathjax: true
---
```

> **注意**：可能会遇到行内公式的渲染问题，参见 [在 Hexo 中使用 MathJax 渲染数学公式 | 苏易北](https://abelsu7.top/2018/10/29/hexo-mathjax/)


### 8. 开启标签页

```bash
hexo new page tags
```

并修改`blog/source/tags/index.md`的元数据：

```yaml
...
...
layout: tags
comments: false
---
```

### 9. 开启分类页

```bash
hexo new page categories
```

并修改`blog/source/categories/index.md`的元数据：

```yaml
...
...
layout: categories
comments: false
---
```


以下是 [hexo-theme-indigo](https://github.com/yscoder/hexo-theme-indigo) 的说明——

----


hexo-theme-material-indigo
================

[![Join the chat at https://gitter.im/hexo-theme-indigo/Lobby](https://badges.gitter.im/hexo-theme-indigo/Lobby.svg)](https://gitter.im/hexo-theme-indigo/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Material Design 风格的Hexo主题，基于 Hexo 3.0+ 制作。 [Preview](http://imys.net/)

> 现有两个主题分支，我的博客中使用的是 card 分支卡片风格主题，master 分支是旧版平铺式风格主题。

## Feature

1. 仅支持 IE10+ 等现代浏览器。
2. 去 jQuery，更轻。相信现代浏览器的原生兼容性。
3. 使用 Less 作为 css 预处理器，需要安装 `hexo-renderer-less`。
4. 添加了英文字体支持 Roboto。
5. 添加了一些波纹效果。By [Waves](https://github.com/fians/Waves)
6. 无前端依赖的分享实现。
7. 基于静态数据的站内搜索，无第三方侵入。
8. 支持文章打赏。

## Useage

[文档 | Document](https://github.com/yscoder/hexo-theme-indigo/wiki)

## ChangeLog

升级前请仔细查看更改内容，如非必要可不升级。

[ChangeLog](https://github.com/yscoder/hexo-theme-indigo/releases)

## OtherVersion

* [vuepress-theme-indigo](https://github.com/yscoder/vuepress-theme-indigo)
