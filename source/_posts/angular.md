---
title: angular 初探
date: 2018-02-16 15:09:47
tags: 
    - angular  
categories: angular
---
# 环境搭建
1. 安装cnpm 
```
npm install cnpm -g --registry=https://registry.npm.taobao.org  
```
<!----more---->

2. 安装angular
- 用cnpm安装@angular/cli
```
npm install -g @angular/cli

cnpm install -g @angular/cli
```
> 这个CLI是Command Line Interface的简写，是一种命令行接口，实现自动化开发流程.它可以创建项目、添加文件以及执行一大堆开发任务，比如测试、打包和发布。  
- 检查版本。输入 ng -v，出现下面的效果，就证明你安装@angluar/cli 成功了。
```
ng -v
```
- 安装失败时
```
npm uninstall -g @angular/cli  //卸载angular/cli 

npm cache clean  //清除缓存

cnpm install -g @angular/cli //重新安装
```

# 创建项目
先到cmd里进入项目所在的目录，用cd命令进入。
1. 新建项目名
```
ng new your_project 
```
2. 进入所建目录启动服务
```
cd your_project
```
```
cnpm install     //安装依赖 
```
```
ng serve --open  //启动服务
```
# 指令
Angualr CLI提供了许多常用命令供我们选择：
```
ng generate class my-new-class              // 新建 class
ng g cl my-new-class                        // 新建 class
ng generate component my-new-component      // 新建组件
ng g c my-new-component                     // 新建组件
ng generate directive my-new-directive      // 新建指令
ng g d my-new-directive                     // 新建指令
ng generate enum my-new-enum                // 新建枚举
ng g e my-new-enum                          // 新建枚举
ng generate module my-new-module            // 新建模块
ng g m my-new-module                        // 新建模块
ng generate pipe my-new-pipe                // 新建管道
ng g p my-new-pipe                          // 新建管道
ng generate service my-new-service          // 新建服务
ng g s my-new-service                       // 新建服务
```
# 构建应用程序
若要构建应用程序，则可以运行：
```
ng build
```
