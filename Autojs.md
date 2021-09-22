# 零、综述

1. 电脑上开发，推送到手机端运行，参见【https://marketplace.visualstudio.com/items?itemName=aaroncheng.auto-js-vsce-fixed】
2. 【自动操作】类模块，【其他】类模块
   - 自动操作模块：基于控件（适用于游戏），基于坐标（适用于软件）

# 一、模块

1. 导出和引入方式

# 二、基于控件的操作

1. to start with 'auto()' or 'auto.waitFor()'.

2. 'SimpleAcitonAutomator' provides api to imitate real actions.

   - click()
   - scrollUp()
   - setText()

3. 'UiSelector' is a fn to get some 'View'.

   - View: ImageView, TextView...

   - Layout: LinearLayout, AbsListView...

   - attributes: text, desc, className...

     ```javascript
     id('hank').findOne().click()			//	find a view which id is hank, and click it to execute a fn
     className('ImageView').depth(10).findOne().click()			//	through many attris to find a view
     ```

   - some  apis to find view:

     ```javascript
     UiSelector.findOne()					//	to find one view till the end
     UiSelector.findOnce()					//	execute one time to find one view
     UiSelector.find()						//	and other fns to find or filter views
     ```

     

4. 'UiObject' is a object got through UiSelector, and can get many attributes