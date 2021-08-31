# 一、基本使用

1. 概念：腾讯出品的小程序快速开发框架，对原生小程序的开发模式进行了再次封装
2. 官网：*[WePY | 小程序组件化开发框架 (wepyjs.github.io)](https://wepyjs.github.io/wepy-docs/)*
3. 优势
   - 开发风格接近【Vue.js】，支持【vue】中许多语法特性
   - 通过【polifill】，让小程序支持【Promise】
   - 可以使用【ES6】等高级语法特性，简化代码，提高效率
   - 优化小程序本身性能
   - 支持第三方的【npm资源】
   - 支持多种插件处理和编译器
4. 安装与初始化
   - 参考文章：*[(13条消息) wepy的基本安装和使用搬砖猴哥-CSDN博客安装wepy](https://blog.csdn.net/weixin_41819098/article/details/103079504?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0.pc_relevant_baidujshouduan&spm=1001.2101.3001.4242)*

# 二、项目介绍

1. 运行编译项目：小程序项目默认存放在【dist目录】中
2. 项目目录：*https://img-blog.csdnimg.cn/20191115094833669.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTgxOTA5OA==,size_16,color_FFFFFF,t_70*
3. 【.wpy】文件的组成部分
   - 脚本部分，<script></script>，其中包括了配置部分（即config对象，json文件部分），逻辑部分（其他js文件部分）
   - 结构部分：<template></template>部分
   - 样式部分：<style></style>部分
   - 小程序入口文件【app.wpy】
4. 小程序入口【app.wpy】
   - config标签：小程序的【app.json】全局配置文件
     - pages数组：小程序的页面
     - window对象：全局配置小程序外观
   - style标签：【app.wxss】样式
   - script标签：【app.js】文件
     - config对象：页面配置对象
     - components对象：页面引入的组件列表
     - data对象：页面模板绑定的渲染数据
     - methods对象：事件函数
     - computed对象：计算属性对象
     - onLoad函数：生命周期函数

# 三、wepy的基本使用

1. 创建页面
   - 【pages文件夹】下创建【wpy文件】，定义基本结构，配置文件路径到【app.wpy】中第一个（首页）
2. 页面绑定事件以及传参
   - @绑定事件，获取事件对象，没有实参且第一个形参为事件对象；或者用【data-自定义属性】传参
3. 文本框和数据绑定同步
   - 插值表达式
4. requets请求
   - 参考文章：*[(13条消息) wepy的基本安装和使用_搬砖猴哥-CSDN博客_安装wepy](https://blog.csdn.net/weixin_41819098/article/details/103079504?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0.pc_relevant_baidujshouduan&spm=1001.2101.3001.4242)*

