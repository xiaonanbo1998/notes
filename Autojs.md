# 零、综述

1. 电脑上开发，推送到手机端运行，参见【https://marketplace.visualstudio.com/items?itemName=aaroncheng.auto-js-vsce-fixed】
2. 【自动操作】类模块，【其他】类模块
   - 自动操作模块：基于控件（适用于游戏），基于坐标（适用于软件）
3. 安装
   - 参考文章：[首页 - AutoX.js (autoxjs.com)](http://doc.autoxjs.com/#/?id=综述)
   - AutoX.js项目地址：[GitHub - kkevsekk1/AutoX: A UiAutomator on android, does not need root access(安卓平台上的JavaScript自动化工具)](https://github.com/kkevsekk1/AutoX)
   - AutoX.js工程项目地址（实现开发、编译、打包、部署、混淆、加密一体化）：[GitHub - kkevsekk1/webpack-autojs](https://github.com/kkevsekk1/webpack-autojs)
   - 安装流程
     - 手机端，安装APP（http://120.25.164.233:8080/appstore/app/20210908180908.apk）
     - 安装【nodejs】，【vs-code】，【插件Auto.js-VSCodeExt-Fixed】（[Auto.js-VSCodeExt-Fixed - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=aaroncheng.auto-js-vsce-fixed)）以及全局下的【webpack】
     - 接下来，参考：[GitHub - kkevsekk1/webpack-autojs](https://github.com/kkevsekk1/webpack-autojs#使用方法)，第三步之后，即第3-6步
   - 运行流程
     - 克隆git文件：https://github.com/kkevsekk1/webpack-autojs.git
     - 安装依赖：【npm install --registry=https://registry.npm.taobao.org】
     - vscode启动服务器：【ctrl + shift + p】+【start server】，同时关闭服务器指令：【stop server】
     - 手机端打开【无障碍服务】，通过【IP地址】连接【同一个无线网或者同一个局域网】的电脑
     - vscode执行【npm run start】，编译并执行代码，在手机端查看；同时支持【热刷新】
4. 新手文章：[Auto.js快速入门实战教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/90065914)

# 一、模块

1. 导出和引入方式

# 二、基于控件的操作

1. 脚本以【无障碍模式】开始：【auto()】或者【auto.waitFor()】

2. 控件选择器

   - 选择控件，举例

     ```javascript
     id('hank').findOne().click()			//	find a view which id is hank, and click it to execute a fn
     className('ImageView').depth(10).findOne().click()			//	through many attris to find a view
     ```

   - 几个【find()函数】的对比

     ```javascript
     UiSelector.findOne()					//	to find one view forever
     UiSelector.findOnce()					//	execute one time to find one view
     UiSelector.find()						//	and other fns to find or filter views
     ```

3. 链式组合，定位控件

   ```javascript
   className("ImageView").depth(10).findOne().click()
   ```

4. 【click(text[, i])】和【uniObject.click()】主要区别

   - 前者【click(text[, i])】，点击文本
   - 后者【UniObject.click()】，点击控件