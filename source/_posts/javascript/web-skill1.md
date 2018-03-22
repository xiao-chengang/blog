---
title: 前端开发技巧一
date: 2018-01-18 15:36:04
tags: 
- web 
- html
- css
categories: web 
---


- 禁用电话、邮箱自动识别
```html
    <meta content="telephone=no" name="format-detection" />
    <meta content="email=no" name="format-detection" />
```

- 获取滚动条的值
```js
    window.scrollY
    window.scrollX
```
<!---more--->
- 禁止选择文本
```css
    -webkit-user-select: none
```

- 重置按钮样式
```css
    -webkit-appearance: none
```

- 多文本换行
```css
    overflow : hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
```

- 快速回弹滚动
在iOS上如果你想让一个元素拥有像 Native 的滚动效果，你可以这样做：
```css
    overflow: auto;
    -webkit-overflow-scrolling: touch;
```
对于body滚动，ios8以上，不加此效果同样拥有弹性滚动效果。

- ios和android局部滚动时隐藏原生滚动条
android:
```css
    ::-webkit-scrollbar{
        opacity: 0;
    }
```
ios:
使用一个稍微高一些div包裹住这个有滚动条的div然后设置overflow:hidden挡住之
```html
    <div class="wrap">
        <div class="box"></div>
    </div>
```
```css
    .wrap{
        height: 100px;
        overflow: hidden;
    }
    .box{
        width: 100%;
        height: -webkit-calc(100% + 5px);
        overflow-x: auto;
        overflow-y: hidden;
        -webkit-overflow-scrolling: touch;
    }
```
