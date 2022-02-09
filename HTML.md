# 零、表情符号

- :carrot:重要内容
- :book:参考
- :ice_cream:细分分类

# 一、网页端的布局

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

2. @media规则：在【媒体查询】中用于不同的媒体类型/设备应用不同的样式（表）

   - 语法

     ```css
     @media not|only mediatype and (mediafeature and|or|not mediafeature) {
         //	CSS-Code;
     }
     ```

     - mediatype：媒体类型

       :ice_cream:all：默认，所有媒体类型设备

       :ice_cream:print：打印机

       :ice_cream:screen：计算机屏幕、平板电脑、智能手机等

       :ice_cream:speech：朗读页面的屏幕阅读器

     - mediafeature：媒体特性，常用的【max-height/显示区域最大高度】等等

   - 案例

     ```html
     <!-- 针对不同的媒体，使用不同的样式表 -->
     <link rel="stylesheet" media="screen and (min-width: 900px)" href="widescreen.css">
     <link rel="stylesheet" media="screen and (max-width: 600px)" href="smallscreen.css">
     ```

     ```css
     //	视口宽度800像素或者更宽，使用【媒体查询】设置背景色为淡紫色
     //	视口宽度介于400至799像素，使用【媒体查询】设置背景色为浅绿色
     //	视口宽度小于400像素，使用【媒体查询】设置背景色为浅蓝色
     body {
         background-color: lightblue;
     }
     @media screen and (min-width: 400px) {
         body {
             background-color: lightgreen;
         }
     }
     @media screen and (min-width: 800px) {
         body {
             background-color: lavender;
         }
     }
     ```

   - :book:参考

     > [CSS @media 规则 (w3school.com.cn)](https://www.w3school.com.cn/cssref/pr_mediaquery.asp)

# 二、伪元素/伪对象和伪类

1. 区分【伪元素/伪对象】和【伪类】：是否创造了新的元素

   - 伪元素：不存在DOM文档中，不存在文档树中，创建了【新元素】，可以通过添加实际的元素来实现，如【a:before】
   - 伪类：存在DOM文档中，存在于文档树中，可以通过添加实际的类来实现，如【a:hover】、【p:nth-child(n)】、【radio:checked】

2. 【:before】和【:after】CSS2的伪元素：用于元素的内容前后加上指定内容

3. 【::before】和【::after】CSS3的伪元素，主要用于区分CSS2的伪元素

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
   
   - :book:参考
   
     > [(15条消息) 伪元素和伪类的区别总结_张木期的博客-CSDN博客_伪类和伪元素](https://blog.csdn.net/qq_27674439/article/details/90608220)

# 三、弹性布局

1. 参考文章：space-evenly：[解决flex布局的space-evenly兼容性问题 - 简书 (jianshu.com)](https://www.jianshu.com/p/bbd114834c59)

2. 【fixed】和【absolute】不会撑大盒子

3. 盒子模型之【box-sizing】属性

   ```css
   .box-style {
       box-sizing: content-box;			//	默认值，宽高只包括内容宽高
       box-sizing: border-box;				//	宽高包括内容，内边距和边框的宽高
   }
   ```

   - :book:参考

     > [box-sizing - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing)


# 四、文字溢出处理

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

4. line-break：auto [, anywhere]，处理带有标点符号的文本行

5. 【word-break】和【overflow-wrap】

   - 【word-wrap 】属性原本属于微软的一个私有属性，在 CSS3 现在的文本规范草案中已经被重名为 【overflow-wrap】 。 【word-wrap】现在被当作 overflow-wrap 的 “别名”。 稳定的谷歌 Chrome 和 Opera 浏览器版本支持这种新语法。
   
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
   
   - :book:参考
   
     > [overflow-wrap - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow-wrap)

# 五、背景图片处理

1. background-size

   ```css
   background-size: 50px 50px;			//	设置背景图片宽高，数值可替换成【auto】或者【百分比】
   background-size: cover;				//	缩放背景图，完全【覆盖】背景区域，至少宽或者高相等，同时保持图片的宽高
   background-size: contain;			//	缩放背景图，完全【装入】背景区域，多余的背景区域，显示背景颜色
   ```
   
   - :book:参考
   
     > [background-size - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size)

# 六、Less语法总结

1. 简介：Less（Leaner Style Sheet）向后兼容的CSS扩展语言，对CSS语言增加了少许扩展

2. 变量/Variables

   - 源码

     ```less
     @width: 10px;
     @height: @width + 10px;
     
     #header {
         width: @width;
         height: @height;
     }
     ```

   - 编译

     ```css
     #header {
         width: 10px;
         height: 20px;
     }
     ```

3. 嵌套/Nesting

   - 源码

     ```less
     #header {
         color: black;
         .navigation {
             font-size: 12px;
         }
         .logo {
             width: 300px;
         }
     }
     ```

   - 编译

     ```css
     #header {
         color: black;
     }
     #header .navigation {
         font-size: 12px;
     }
     #header .logo {
         width: 300px;
     }
     ```

   - :carrot:案例

     ```less
     //	clearfix案例
     .clearfix {
         display: block;
         zoom: 1;
         
         &:after {
             content: "";
             display: block;
             font-size: 0;
             height: 0;
             clear: both;
             visibility: hidden;
         }
     }
     ```

   - :carrot:【@规则】嵌套和【冒泡/bubbling】：@规则会被放在前面，同一规则集中的其他元素的相对顺序保持不变，即【冒泡】

     - 源码

       ```less
       .component {
           width: 300px;
           @media (min-width: 768px) {
               width: 600px;
               @media (min-resolution: 192dpi) {
                   background-image: url(/img/retina2x.png);
               }
           }
           @media (min-width: 1280px) {
               width: 800px;
           }
       }
       ```

     - 编译

       ```css
       .component {
           width: 300px;
       }
       @media (min-width: 768px) {
           .component {
               width: 600px;
           }
       }
       @media (min-width: 768px) and (min-resolution: 192dpi) {
           .component {
               background-image: url(/img/retina2x.png);
           }
       }
       @media (min-width: 1280px) {
           .component {
               width: 800px;
           }
       }
       ```

4. :book:参考

   > [Less 快速入门 | Less.js 中文文档 - Less 中文网 (bootcss.com)](https://less.bootcss.com/)
