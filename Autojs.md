# 零、综述

1. 电脑上开发，推送到手机端运行，参见【https://marketplace.visualstudio.com/items?itemName=aaroncheng.auto-js-vsce-fixed】
3. 安装
   - 参考文章：[首页 - AutoX.js (autoxjs.com)](http://doc.autoxjs.com/#/?id=综述)
   - 环境：node@12.20.0，npm@6.14.8
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
     - 手机端打开【无障碍服务】，通过【IP地址】连接【同一个局域网】的电脑
     - vscode执行【npm run start】，编译并执行代码，在手机端查看；同时支持【热刷新】
     - vscode执行【npm run build】，编译并发布/构建代码，便于手机端打包发布APK，再【签名打包】
3. 新手文章：[Auto.js快速入门实战教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/90065914)

# 一、模块

1. 导出和引入方式

   ```javascript
   //	file1.js，文件一内容，导出定义的东西
   var demo = {
       start: function() {
           console.log('This is a demo...')
       }
   }
   module.exports = demo
   
   //	file2.js，文件二内容，引入想要的文件内容
   const Demo = require('./file1')			//	写法一
   const Demo = require('./file1.js')		//	写法二
   ```

2. 导出的内容：【函数】或者【对象】，添加到【引入模块】的根部

# 二、常用函数

1. click()函数

   ```javascript
   //	基于控件的click()函数
   let res = text('Autox.js').findOne().click()
   console.log(res)			//	true || false，如果该控件不可点击（clickalbe = false），则返回false
   
   //	基于控件的SimpleActionAutomator()函数，【click(text[, i])】
   let res = click('Autox.js', 0)
   console.log(res)			//	true || false，点击文字区域（从文本处向父视图寻找），不可点击（clickalbe = false），则返回false
   
   //	基于坐标的click(x, y)函数
   let res = click(200, 400)
   console.log(res)			//	true || false，点击坐标(x, y)，【如果父视图可以点击（clickalbe = true）】，则返回true
   
   //	举例：
   //	1、click(x, y)，可以找父视图
   let btn = text('教程').findOne().bounds()
   let xx = btn.centerX()
   let yy = btn.centerY()
   let res = click(xx, yy)
   console.log('xx, yy, res: ', xx, yy, res)               //  success
   //	2、click()，不可以找父视图
   let btn = text('教程').findOne()
   let res = btn.click()
   console.log('res: ', res)                               //  fail
   //	3、click(text[, index])，可以找父视图
   let res = click('教程', 0)
   console.log('res: ', res)                               //  success
   ```
   
2. text()函数、textContains()函数、textMatches(reg)函数

   ```javascript
   text('微信')					//	匹配“微信”文本，返回UniSelector对象
   textContain('微')			//	匹配“微信”，“微信号”等包含“微”的文本，返回UniSelector对象
   textMatches(/微信|腾讯/)		//	匹配“微信”和“腾讯”文本，reg需要满足正则表达式，返回UniSelector对象
   ```

3. desc()函数，depth()函数、类似text()函数，匹配UniSelector的desc属性

   ```javascript
   desc('微信')			//	匹配desc属性值，返回UniSelector对象
   depth(12)			//	匹配depth属性值，返回UniSelector对象
   ```

   

4. findOne()函数、findOnce()函数、find()函数、waitFor()函数

   ```javascript
   text('Autox.js').findOne()			//	寻找满足条件的控件，直到出现，以及采用深度优先/DFS搜索方式，返回UniSelector对象
   text('Autox.js').findOne(5000)		//	寻找满足条件的控件，5秒内，没有则返回null
   text('Autox.js').findOnce()			//	当下，寻找满足条件的控件，返回UniSelector对象，没有则返回null
   text('Autox.js').find()				//	当下，寻找满足条件的所有控件，返回UniCollection
   text('Autox.js').waitFor()			//	等待控件出现，否则阻塞
   ```

5. UniSelector对象、UniCollection对象的方法

   ```javascript
   text('Autox.js').findOne().child(0)			//	寻找第一个子控件
   text('Autox.js').findOne().parent()			//	寻找父控件
   let tap = text('Autox.js').findOne().bounds()			//	返回Rect对象，配合click(x, y)使用，详情如下
   let xx = tap.centerX()
   let yy = tap.centerY()
   tap = click(xx, yy)
   ```

6. launchApp()函数、laungchPackage()函数

   ```
   launchApp("微信")					//	启动应用名称为“微信”的应用
   laungchPackage("com.tencent.mm")	//	启动应用包名为“com.tencent.mm”的应用
   ```

   

7. 其他

   ```
   toast('hello AutoX.js')			//	以气泡的方式显示信息几秒
   sleep(2000)						//	脚本暂停运行2秒
   home()							//	模拟按下Home键，返回true/false
   back()							//	模拟按下返回键，返回true/false
   ```

8. 提示：

   - 慎用退出、紧密逻辑、多打日志、多方测试（开发测试，发布手机测试，打包测试，多手机测试）
   - 命名：不用大小写，使用短横线

# 三、Scheme

1. 参考网址： [(29 封私信 / 80 条消息) 你所知道好玩有趣的 iOS URL Scheme 有哪些？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/19907735/answer/227302030) 
2. 参考网址： [(26条消息) 常见软件的Scheme_小钢炮的博客-CSDN博客](https://blog.csdn.net/fwx426328/article/details/108241829) 
3. 参考网址： [(26条消息) 常用URL schemes ✨支付宝 、微信、腾讯、百度、网易、银行 、社交 、音频 、工具大集合_时光不染-CSDN博客](https://blog.csdn.net/hzhnzmyz/article/details/119149058?utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-7.no_search_link&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-7.no_search_link) 
4. 参考网址（手动获取URL）： [如何找出APP的URL Scheme - 简书 (jianshu.com)](https://www.jianshu.com/p/2271ca5881e1) 
5. 常用
   - 微信：weixin://
   - 网易云音乐： orpheus:// 
   - 喜马拉雅：iting://open
   - 支付宝：alipays://platformapi/startapp?appId=20000001

