---
title: hexo个人博客基础配置
date: 2020-10-27 15:26:23
tags:
- hexo
categories:
- hexo
---
![](/images/facade.jpg) <!-- more -->

# 创建初始项目

## 创建hexo

根据官网 https://hexo.io/zh-cn/docs/ 安装hexo

创建初始项目
```nodejs
hexo init
```

## 使用next主题
next官网 http://theme-next.iissnan.com/getting-started.html
[月小水长的githuab](https://github.com/inspurer/hexo)，里面有很多hexo的使用方法, 如搜索、面版娘、点击爱心等

注意事项：
1. hexo在5.0之后把swig给删除了需要自己手动安装
2. next主题在使用menu菜单时，需要将 'about: /about/ || user' 中'||'前面的空格去掉，否则在点击导航菜单时会出现这种问题 'http://localhost:4000/about/%20'


# 进阶配置

## 使用本地图片
1. 调整配置文件_config.yml里的post_asset_folder为true
2. 在source下创建images文件夹，将图片xx.jpg/png复制到文件夹下
3. 在xxxx.md中引入文件
```markdown
![想输入的提示名字，可不输入](/images/xx.jpg)
```

## 如何折叠（显示/隐藏）部分内容
1. 安装[hexo-sliding-spoiler](https://github.com/fletchto99/hexo-sliding-spoiler)
2. 自定义显示/隐藏文字
打开文件 hexo\node_modules\hexo-sliding-spoiler\assetsspoiler.css，找到25-31行，修改其中的 content
```CSS
.spoiler.collapsed .spoiler-title:before {
	content: "Show: ";
}
.spoiler.expanded .spoiler-title:before {
	content: "Hide: ";
}
```
3. 使用
```markdown
{% spoiler "隐藏内容的标题" %}
|文字|文字|
|-|-|
|文字|文字|
{% endspoiler %}
```
4. 原作者[博客地址](https://www.baidu.com/link?url=DqdoMiVgNqu15TmcORF2gBoRTNAjJkByw73jC8gZZ11g0e1xqmZt09k6QlsYLeE7E31KfB-4yrzdAGvi-jv5TFO_PGRv1y79ChwH6rkF1rW&wd=&eqid=a374ad7600025f1e000000065f97e0d2)

## 添加search本地搜索功能
1. 安装 npm install hexo-generator-searchdb --save
2. 在_config.yml中配置
{% spoiler "隐藏内容的标题" %}
```makedown
search:
  path: search.xml
  field: post
  format: html
       limit: 10000
```
{% endspoiler %}
3. 在主题配置文件/themes/next/_config.yml中，找到 Local search，将 enable 设置为 true，启动本地搜索功能。

## 添加二次元动图面版娘
1. npm install --save hexo-helper-live2d
2. 在站点的配置文件下加入配置
{% spoiler "_config.yml面版娘配置" %}
```makedown
# 二次元图片
live2d:
  enable: true
  scriptFrom: local
  model:
    scale: 1
    hHeadPos: 0.5
    vHeadPos: 0.618
  display:
    superSample: 2
    width: 150
    height: 300
    position: right
    hOffset: 0
    vOffset: -20
  mobile:
    show: false
  react:
    opacityDefault: 0.5
    opacityOnHover: 0.2
```
{% endspoiler %}


## 添加页面点击出现爱心效果
1. 在/themes/next/source/js/src下添加文件love.js
2. 在\themes\next\layout\_layout.swig文件末尾添加
```HTML
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/love.js"></script>
```




