# 零、总纲

1. 网页端布局

   - 设计图分辨率一般是1920*1080，但是浏览器正常视图下分辨率小于这个数值。因此，布局设计时分辨率要适当缩小

   - 具体注意点

     ```css
     body {			//	消除各浏览器自带的内外边距    
         margin: 0;
         padding: 0;
     }
     .container {
         width: 100%;			//	继承父元素，往往是body宽度，body往往是1920px宽度
         height: 100%;			//	根据内容伸缩
         width: 100vw;			//	窗口可视宽度
         height: 100vh;			//	窗口可视高度
     }
     .box {						//	content-box盒子模型，在F12查看下，鼠标选中，提示的宽高为600*500，即内边距在计算中，外边距除外
         margin-top: 100px;
         padding-left: 100px;
         width: 500px;
         height: 500px;
     }
     ```

     

# 一、伪元素/伪对象和伪类

1. 区分【伪元素/伪对象】和【伪类】：是否创造了新的元素

   - 伪元素：不存在DOM文档中，不存在文档树中，可以通过添加实际的元素来实现
   - 伪类：存在DOM文档中，存在于文档树中，可以通过添加实际的类来实现

2. 【:before】和【:after】CSS2的伪元素：用于元素的内容前后加上指定内容

3. 【::before】和【::after】CSS3的伪元素，主要用于区分CSS2的伪类

4. 伪元素的使用

   - 清除浮动

     ```css
     ul:after {
     	content: '';
     	display: block;
     	width: 0;
     	height: 0;
     	clear: both;
     }
     /*或者*/
     .clearfix {*zoom: 1;}
     .clearfix:before,.clearfix:after {display: table;line-height: 0;content: "";}
     .clearfix:after {clear: both;}
     ```

   - 制作三角形

     ```css
     .demo:after{
         content: '';
         display: inline-block;
         width: 0;
         height: 0;
         border: 8px solid transparent;
         border-left: 8px solid #AFABAB;
         position: relative;
         top: 2px;
         left: 10px;
     }
     ```

5. 备注

   - 【display: table;】，宽度自适应内容，块级元素
   - 【display: table-cell;】
   - 参考文章：[(15条消息) 伪元素和伪类的区别总结_张木期的博客-CSDN博客_伪类和伪元素](https://blog.csdn.net/qq_27674439/article/details/90608220)

# 二、弹性布局

1. 参考文章：space-evenly：[解决flex布局的space-evenly兼容性问题 - 简书 (jianshu.com)](https://www.jianshu.com/p/bbd114834c59)

2. 【fixed】和【absolute】不会撑大盒子

3. :ice_cream:盒子模型之【box-sizing】属性

   ```css
   .box-style {
       box-sizing: content-box;			//	默认值，宽高只包括内容宽高
       box-sizing: border-box;				//	宽高包括内容，内边距和边框的宽高
   }
   ```

   > 参考：[box-sizing - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing)

4. 留白

# 三、文字溢出处理

1. overflow：visible [, hidden]，处理溢出

2. white-space: normal [, nowrap]，处理元素中空白

3. text-overflow：clip(默认值) [, ellipsis]，处理溢出内容展示

   ```css
   .txt {						//	效果：汉字单行显示，溢出内容【...】代替
       overflow: hidden;
       white-space: nowrap;
       text-overflow: ellipsis;
   }
   ```

4. :carrot:line-break：auto [, anywhere]，处理带有标点符号的文本行

5. :carrot:【word-break】和【overflow-wrap】

   - :notebook:【word-wrap 】属性原本属于微软的一个私有属性，在 CSS3 现在的文本规范草案中已经被重名为 【overflow-wrap】 。 【word-wrap】现在被当作 overflow-wrap 的 “别名”。 稳定的谷歌 Chrome 和 Opera 浏览器版本支持这种新语法。
   
   ```css
   .English-word {		//	针对英语
       word-break: normal;		//	可以溢出
       word-break: break-all;	//	截断单个单词，并换行
       word-break: break-word;	//	不截断单词，换行
   }
   .English-word {
       overflow-wrap: normal;		//	在正常断点处中断换行
       overflow-wrap: break-word;	//	截断单词，并换行
   }
   ```
   
   > 参考：[overflow-wrap - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow-wrap)

# 四、背景图片处理

1. :carrot:background-size

   ```css
   background-size: 50px 50px;			//	设置背景图片宽高，数值可替换成【auto】或者【百分比】
   background-size: cover;				//	缩放背景图，完全【覆盖】背景区域，至少宽或者高相等，同时保持图片的宽高
   background-size: contain;			//	缩放背景图，完全【装入】背景区域，多余的背景区域，显示背景颜色
   ```

> [background-size - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size)

