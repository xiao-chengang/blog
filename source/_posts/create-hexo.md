---
title: Hexo搭建GitHub博客
date: 2018-02-20 10:55:19
tags: 
- hexo 
- blog 
- 教程
categories:  hexo
excerpt: test
---
# Hexo简介
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
<!------more----->


# 基础配置篇
**【注：本文中使用的 Hexo 版本为3.22，部分配置与2.x可能有所出入】**
1. 安装 & 搭建

- 安装Git：安装后，注册 Github 账号，配置 SSH（具体见下一步）,打开 Git Bash,- 接下来的命令均在Git Bash中执行
- 安装Node.js
- 安装 Hexo : $npm install -g hexo
- 安装依赖包： $npm install
- 新建博客文件夹：cd到该文件夹，执行$hexo init
- 新建Github仓库：仓库名必须为你的Github名.github.io，要不然就不能使用Github Pages服务了。。。
------
2. 配置 SSH

    关于什么是 SSH，请自行百度（我懒..）这里直接讲一下配置步骤。

- 本地生成公钥私钥 
```
　$ssh-keygen -t rsa -C "你的邮件地址"
```
- 添加公钥到 Github 
    * 根据上一步的提示，找到公钥文件（默认为id_rsa.pub），用记事本打开，全选并复制。
    * 登录 Github，右上角 头像 -> Settings —> SSH keys —> Add SSH key。把公钥粘贴到key中，填好title并点击 Add key。
    * git bash中输入命令$ssh -T git@github.com，选yes，等待片刻可看到成功提示。
-----
3. NexT主题下载  
    NexT 主题是由 iissnan 大神所制作的一款简洁美观不失逼格的主题。下载方法有以下两种：
- 进入博客根目录`/themes/`, 执行`$git clone `
```
https://github.com/iissnan/hexo-theme-next.git
```
- 直接进入上面的链接，在项目主页download zip文件，然后解压到`博客根目录/themes/`文件夹
-----
4. 发布
    使用以下两条命令进行发布，发布成功后可在浏览器中使用你的github名.github.io进入你的博客~
```
$hexo clean
$hexo d -g
```
-----
# Hexo日常使用篇
1. 生成静态页面：
```
$ hexo generate
$ hexo g
```
2. 本地预览：
```
$hexo server//或 hexo s
//然后打开浏览器输入localhost:4000可以预览博客效果，用于调试
```
3. 新建文章
```
$hexo new post "title"
//新文章位置：/source/_posts
```

4. 新建页面
```
$hexo new page "title"
```

5. 部署并生成
```
$hexo d -g
```
6. 清除生成的文件和缓存
```
$hexo clean
```
-----
# _config文件配置篇
## 1.整站配置
请参照[hexo官网配置](https://hexo.io/zh-cn/docs/configuration.html)
## 2.Next主题配置
请参照[next主题配置](http://theme-next.iissnan.com/theme-settings.html#tags-page)
# 个人定制模块
## 更改代码块颜色及字体大小
1. 打开\themes\next\source\css\ _variables\base.styl文件
2. 修改$code-background和$code-foreground的值：
```
// Code & Code Blocks
// 用``围出的代码块
// --------------------------------------------------
$code-font-family               = $font-family-monospace
$code-font-size                 = 15px # 代码字体大小
$code-background                = #自定义RGB值
$code-foreground                = #自定义RGB值
$code-border-radius             = 4px
```