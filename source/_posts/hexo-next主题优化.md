---
title: 【持续更新】hexo next主题优化手册
copyright: true
date: 2018-11-11 21:24:19
tags: [hexo, next]
categories: hexo
top: 100
---
![](https://i.imgur.com/4O4llpT.png) <!-- more -->           
# 前言   
## 开此贴的原因    
前几天博客崩了，重新搭建了这个博客站点。    
特开此贴记录next主题优化过程中遇到的问题，希望对大家有所帮助。
## 一些说明
前期相关的Hexo安装、本地/远程部署教程可百度在此不再赘述。   
基于hexo-next v5.1.4,向上兼容,向下兼容性不确定，特此声明。  
我的博客本地根目录是`D:\hexoblog`     
站点配置文件全路径是`‪D:\hexoblog\_config.yml`   
next主题文件全路径是`‪D:\hexoblog\themes\next\_config.yml`  
## hexo常见操作      
`hexo new "postName"` #新建文章    
`hexo new page "pageName"` #新建页面    
`hexo clean` #清除部署緩存    
`hexo n == hexo new` #新建文章     
`hexo g == hexo generate` #生成静态页面至public目录     
`hexo s == hexo server` #开启预览访问端口（默认端口4000，可在浏览器输入`localhost:4000`预览）    
`hexo d == hexo deploy` #将.deploy目录部署到GitHub     
`hexo g -d` #生成加部署      
`hexo g -s` #生成加预览    

----

# next主题优化    
## next风格选择    
next有四种风格,在站点配置文件搜索字段`Scheme Settings`可以看到，  


	# Scheme Settings
	# ---------------------------------------------------------------
	# Schemes
	#scheme: Muse
	#scheme: Mist
	#scheme: Pisces
	scheme: Gemini
    
我这里用的是四种：`Gemini`     
## next菜单设置   
比如可以看到我的主页有`首页`、`留言`、`分类`、`归档`、`标签`等菜单，      
在站点配置文件下搜索`menu:`,可以看到   

	menu:
      home: / || home
      about: /about/ || user
      message: /message/ || comment
      tags: /tags/ || tags
      categories: /categories/ || th
      archives: /archives/ || archive
      #schedule: /schedule/ || calendar
      #sitemap: /sitemap.xml || sitemap
      #commonweal: /404/ || heartbeat
`home`就是`首页`;`message`就是`留言`...一开始只有首页和归档,其余的需要我们手动创建，   
在站点根目录下打开命令行,输入`hexo new page "about" `     
并在主题配置文件`menu:`字段处取消对about的注释     
重新部署我们就可以看到主页有`关于`这个菜单了，其他的类似，     
修改`D:\hexoblog\source\about\index.md`,就可以修改`关于`界面了   
`about: /about/ || user`中的`user`是指`关于`菜单附件的图标用的是[图标库](https://fontawesome.com/icons?from=io)里面名为`user`的图标   
## 添加萌妹子动图   
### 在根目录下打开命令行   
输入`npm install --save hexo-helper-live2d`   
### 修改站点配置文件(注意不是主题配置文件)    
在末尾加入:    
 
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
    		opacityOnHover: 0.

## 实现文章首页"分类于"、"阅读次数"等效果    
效果图如下:    
![](https://i.imgur.com/sIHtbOe.png)     
### 在根目录下打开命令行  
依次输入以下命令:    
	  
	npm install hexo-wordcount --save
	npm uninstall hexo-generator-index --save
	npm install hexo-generator-index-pin-top --save   
### 打开主题配置文件   
打开相关开关:   
	
	post_wordcount:
		item_text: true
		wordcount: true
		min2read: true
		totalcount: true
### 打开.../themes/next/layout/_macro/post.swig文件   
把里面的代码用下面的代码替换:     
[点击下载](https://pan.baidu.com/s/1W_mDJXS3gDs_iq1aQEZaaA)    
### 打开.../themes/next/languages/zh-Hans.yml文件   
搜索`post`字段,添加一行`comments: 评论数`,注意其余的不要改   

### 设置某篇文章置顶   
前面的流程走完后,只需要在写文章的时候在文章前面加入top: true    
或者top: 100(100只是个例子，数字越大越靠前),就能实现置顶效果了    

---
# 常见错误    
## 本地预览和同时发布到远程的浏览结果不一致    
这是由缓存造成的,需要先`hexo clean`,再`hexo g -d`部署到远程    

---
# markdown高级语法    
## 插入连续多行的代码块    
按一个tab键,然后贴代码，保证每一行代码前都要额外的tab键,同时最前面空一行。    
比如,我前面插入的连续行代码的实现效果:      
![](https://i.imgur.com/Z0BCMhF.png)      

## 设置文字大小和颜色和居中效果   
hello,world!    
<font color="#FF0000"> hello,world! </font>    
<font size=5> hello,world! </font>     
<font size=5 color="#FF0000">hello,world! </font>    
<center>hello,world!</center>   
上面的效果需要在markdwon中的代码是这样的:   

	hello,world!    
	<font color="#FF0000"> hello,world! </font>    
	<font size=5> hello,world! </font>     
	<font size=5 color="#FF0000">hello,world! </font>    
	<center>hello,world!</center>    
## 插入表格  
效果图:   

| 左对齐标题 | 右对齐标题 | 居中对齐标题 |
| :------| ------: | :------: |
| 短文本 | 中等文本 | 稍微长一点的文本 |
| 稍微长一点的文本 | 短文本 | 中等文本 |

markdown代码如下：    

	| 左对齐标题 | 右对齐标题 | 居中对齐标题 |
	| :------| ------: | :------: |
	| 短文本 | 中等文本 | 稍微长一点的文本 |
	| 稍微长一点的文本 | 短文本 | 中等文本 |

---
# 感谢赞助        
所有赞赏过本站的人: [点击查看](https://inspurer.github.io/thank/)   
 





