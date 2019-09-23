---
title: hexo入门
date: 2019-07-15 13:54:15
tags: [hexo]
categories: hexo搭建
---

## 常用命令

1. 创建新文章
`hexo new post title`

2. 本地运行
`hexo s`

3. 生成静态文件
`hexo g`

## hexo插件

1. 本地上传图片 `hexo-asset-image ^0.0.1` 

0.0.1版本可用，默认的1.0.0版本默认路径错误。

2. 代码高亮 `highlight.js`

引入js和css在路径 `themes\next\layout\_partials\head\head.swig` 和 `themes\next\layout\_partials\footer.swig` 下。<br/>

代码高亮padding设置在`themes\next\source\css\_common\components\highlight\highlight.styl`下

