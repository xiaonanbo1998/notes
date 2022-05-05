# 符号注释

- :book:注释
- :snowflake:一般分类
- :question:问题

# 一、Flutter指令 及框架

1. 参考文章：[(28条消息) Flutter常用命令行_大灰狼的小绵羊哥哥的博客-CSDN博客_flutter 命令](https://blog.csdn.net/sinat_17775997/article/details/106418282)

2. 常用指令

   ```git
   flutter run			//	运行项目
   flutter pub get		//	获取依赖项
   flutter upgrade		//	升级SDK
   flutter channel beta	//	切换到beta版本，一共有beta、stable、master版本
   ```
   
   
   
3. :book:参考

   > 生命周期：[[Flutter\] 10-Flutter的生命周期 - 简书 (jianshu.com)](https://www.jianshu.com/p/6ed6f7de01ff)
   >
   > SDK升级：[升级你的 Flutter 版本 | Flutter 中文文档 | Flutter 中文开发者网站](https://flutter.cn/docs/development/tools/sdk/upgrading)
   >
   > 代理配置，镜像网站：[在中国网络环境下使用 Flutter | Flutter 中文文档 | Flutter 中文开发者网站](https://flutter.cn/community/china)
   >
   > 第三方插件库：[Flutter第三方插件汇总（持续更新） - 掘金 (juejin.cn)](https://juejin.cn/post/6874082988381241357#heading-20)

# 二、第一个Flutter应用

1. 计数器应用示例

2. Widget简介

3. 状态管理

4. :book:参考

   > Flutter实战-第二版：[第二版序 | 《Flutter实战·第二版》 (flutterchina.club)](https://book.flutterchina.club/)

# 三 、布局类组件

1. 组件分类

   |            Widget             |       说明       |                             用途                             |
   | :---------------------------: | :--------------: | :----------------------------------------------------------: |
   |    LeafRenderObjectWidget     | 非容器类组件基类 | Widget树的叶子节点，没有子节点，通常基础组件都属于这一类，如Image |
   | SingleChildRenderObjectWidget |   单子组件基类   |      包含一个子组件，如：ConstrainedBox、DecoratedBox等      |
   | MultiChildRenderObjectWidget  |   多子组件基类   | 多个子组件，一般都有一个children参数，接受一个Widget数组，如：Row、Column、Stack等 |

2. :snowflake:两种布局模型

   - 基于【RenderBox】的盒模型布局
   - 基于【RenderSliver/Sliver】的按需加载列表布局

3. 盒模型的约束组件

4. 线性布局（Row和Column）

   - 主轴方向，尽可能大；纵轴方向取决于子元素长度
   - 嵌套使用时，里面的【Row/Column】占用的空间大小为实际大小

5. 弹性布局（Flex、Expanded、Row和Column）

6. 流式布局（Wrap和Flow）

7. 层叠布局（Stack和Positioned）

   - 【Stack组件】，允许子组件堆叠；【Posintioned】，根据Stack四个角确定子组件位置
   - 【Align组件】通过【Alignment类和FractionalOffset类】计算偏移

# 四、容器类组件

1. 填充（Padding）
2. 装饰容器（DecoratedBox）
3. 变换（Transform）
4. 普通多组合容器（Container）
5. 剪裁（Clip）
6. 空间适配 （FittedBox）
7. 默认容器（Scaffold）

# 五、可滚动组件

1. 可滚动组件简介

   - 可滚动的组成

     :snowflake:Scrollable：处理滑动手势，确定滑动偏移，偏移时构建Viewport

     :snowflake:Viewport：显示的视窗，即列表的可视区域

     :snowflake:Sliver：视窗里显示的元素

   - ScrollController：配置controller属性，控制可滚动组件的滚动

   - Scrollbar：Material风格的滚动指示器/滚动条

2. SingleChildScrollView：在期望内容不会超出屏幕太多使用

3. ListView

   - 默认构造函数：适用于少量组件
   - ListView.builder：适用于多项组件，按需加载
   - ListView.separated：生成的列表项之间添加一个分割组件

4. 滚动监听及控制

   - ScrollController：控制滚动的类

5. AnimatedList

   - AnimatedList：在列表中插入或删除节点时，执行一个动画

6. GridView

7. PageView与页面缓存

   - PageView：实现页面切换和Tab布局
   - 页面缓存

8. 可滚动组件子项缓存KeepAlive

9. TabBarView

10. CustomScrollView和Slivers

    |        Sliver名称         |                功能                |       对应的可滚动组件        |
    | :-----------------------: | :--------------------------------: | :---------------------------: |
    |        SliverList         |                列表                |           ListView            |
    |   SliverFixedExtentList   |           高度固定的列表           |  ListView，指定itemExtent时   |
    |    SliverAnimatedList     |    添加/删除列表项可以执行动画     |         AnimatedList          |
    |        SliverGrid         |                网格                |           GridView            |
    | SliverPrototypeExtentList |     根据原型生成高度固定的列表     | ListView，指定prototypeItem时 |
    |    SliverFillViewport     | 包含多个子组件，每个都可以填满屏幕 |           PageView            |

    - CustomScrollView 组合 Sliver 的原理是为所有子 Sliver 提供一个共享的 Scrollable，然后统一处理指定滑动方向的滑动事件
    - CustomScrollView 和 ListView、GridView、PageView 一样，都是**完整**的可滚动组件（同时拥有 Scrollable、Viewport、Sliver）
    - CustomScrollView 只能组合 Sliver，如果有孩子也是一个**完整**的可滚动组件（通过 SliverToBoxAdapter 嵌入）且它们的滑动方向一致时便不能正常工作

11. 自定义Sliver

12. 嵌套可滚动组件NestedScrollView

    - NestedScrollView整体是一个CustomScrollView（的子类）

# 三、Packages的开发和提交

1. 【Packages】和【插件/plugin】区别
   - 【plugin】是【package】的一种，全称是【plugin package】，简称【插件/plugin】
   - 【Dart packages】最低要求包含一个【pubspec.yaml文件】，可以包含依赖关系（有Dart库、应用等等）
   - 【plugin package】主要用来获得原生平台的API或者相关特性等等
   
2. 添加依赖（[Flutter 中文文档 - Flutter 中文资源 | 在 Flutter 里使用 Packages](https://flutter.cn/docs/development/packages-and-plugins/using-packages#developing-new-packages)）
   - 通常：在【pubspec.yaml】添加package，安装依赖，导入依赖
   
3. 管理依赖
   - Hosted packages（org）：发布到【pub.darlang.org】的依赖
   - Git packages（远端）：在git等远端管理的依赖
   - Path packages（本地）：存在本地的依赖
   
4. 内容：【pubspec.yaml文件】、【lib目录】

5. 类别：【纯Dart库/Dart package】插件、【原生插件/ Plugin package】插件

6. Plugin package

   - 联合插件：将对不同平台支持的功能分为单独的软件包
   - 内容：面向应用的package，平台package，平台接口package
   - 引入方式
   
7. 撰写双端平台代码：编写自定义平台的相关代码
   - 原理：flutter在【客户端/UI】通过【平台通道】向【宿主/其他平台】发送消息，【宿主/其他平台】通过【平台通道】接收消息，调用【宿主/其他平台】的API，实现相关功能
   - 案例：[Flutter 中文文档 - Flutter 中文资源 | 撰写双端平台代码（插件编写实现）](https://flutter.cn/docs/development/platform-integration/platform-channels?tab=android-channel-java-tab#codec)
   - 实现方式
     - 通过【插件】的方式，调用Native API：关键类是【FlutterPlugin】和【MethodCallHandler】。应用层可以直接调用插件封装好的API，调用Native API——参考案例：【项目hello】
     - 通过自身实现Native API：关键类是【FlutterEngine】。应用层调用服务层的API，但是服务层的API调用Native API的步骤，需要开发者自己实现，算得上真正意义上的【双端平台】的开发——参考项目：【项目get_android_version】
   
8. 引入【Andorid端】第三方框架/插件

   ```groovy
   //	例如引入【EasyFloat】框架
   //	1、项目根目录【build.gradle】，添加如下代码
   allprojects {
   	repositories {
   		...
   		maven { url 'https://jitpack.io'}	//	关键代码
   	}
   }
   //	2、应用模块【build.gradle】，添加如下代码
   dependencies {
       implementation 'com.github.princekin-f:EasyFloat:2.0.3'	//	关键代码
   }
   ```

   

# 四、无障碍服务

1. 概括：简单说，就是一个后台监控服务，根据监控内容，调用后台的回调方法
   
2. 关键词（[详解安卓辅助功能服务AccessibilityService（无障碍服务，微信抢红包助手原理） - 简书 (jianshu.com)](https://www.jianshu.com/p/e1ba386464ad)）

   - AccessibilityEvent：事件
   - AccessibilityManagerService（AMS）：分发事件的服务管理
   - AccessibilityManager（AM）：发送事件（的APP）
   - AccessibilityService（AS）：有无障碍服务（的APP）

3. AM与AMS与AS之间的通信

   - AM与AMS通信：AM是单例模式，调用【tryConnectToServiceLocked()函数】，连接AMS并通信

   - AMS与AS通信：【设置->无障碍模式】通知状态变化，进而调用AMS的【onUserStateChangedLocked()函数】，其中主要关于【updateServicesLocked()函数】处理无障碍服务绑定，其涉及多个AMS类内部集合，最终会调用【bindlock()函数】进行对应的无障碍服务绑定；AS则通过【onBind()函数】与AMS中的【AccessibilityServiceConnection】进行通信

   - 图示

     ![img](https://upload-images.jianshu.io/upload_images/5714046-66a3d45196168203.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

4. 关于事件监听

   - 触发：（模拟）点击———创建AM实例并绑定———生成并初始化Event———通过AMS获取本地Binder——发送Event

   - 分发：维护AS的表——遍历表获取serviceconnection——调用函数分发到AS

   - 回调：重写方法，实现操作

   - 图示

     ![img](https://upload-images.jianshu.io/upload_images/5714046-ecc1ea6ba751f892.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

5. 如何开发

   1. :snowflake:创建服务类：继承【AccessibilityService类】，重写【onServiceConnected()】、【onAccessibilityEvent()】和【onInterrupt()】方法

      - onServiceConnected()：系统成功绑定时触发，一次性，必须
      - onUnbind()：系统关闭服务时触发，一次性，可选
      - onAccessibilityEvent()：监听事件成功则触发，多次，必须
      - onInterrupt()：中断AS反馈时触发，反馈有震动、音频等，即在执行无障碍服务中，服务被中断，则触发此函数，多次，必须

   2. :snowflake:在【AndroidManifest.xml】声明服务，配置参数
      - 配置【<intent-filter>】
      
      - 声明【BIND_ACCESSIBILITY_SERVICE】权限
      
      - 显示服务名字【android:label】

      - 配置参数方法一：通过【meta-data】标签，指定xml文件进行配置（指定【无障碍服务】处理的事件类型和附加信息，包含在【AccessibilityServiceInfo()类中】）
      
        ```xml
        <service android:name=".MyAccessibilityService"
        	android:exported="true"
        	android:label="@string/accessibility_service_label"
        	android:permission="android.permission.BIND_ACCESSIBILITY_SERVICE">
        	<intent-filter>
        		<action android:name="android.accessibilityservice.AccessibilityService"/>
        	</intent-filter>
        	<meta-data
        		android:name="android.accessibilityservice"
        		android:resource="@xml/demo_config"/>
        </service>
        ```
      
      - 配置参数方法二：通过代码，动态配置参数
      
   3. :snowflake:跳转无障碍服务，再手动授权【无障碍模式】

      ```java
      Intent intent = new Intent(Setting.ACTION_ACCESSIBILITY_SETTING);
      startActivity(intent);
      ```

   4. :snowflake:处理事件信息

      - 处理事件信息的函数是【onAccessibilityEvent(AccessibilityEvent event)】
      - 【AccessibilityEvent()类】封装了界面相关事件的信息，根据不同情况，再执行不同操作

   5. :snowflake:获取节点信息

      - 通过【AccessibilityNodeInfo()类】，控制节点，进行相关操作

   6. 模拟节点相关操作：[AccessibilityNodeInfo  | Android Developers (google.cn)](https://developer.android.google.cn/reference/android/view/accessibility/AccessibilityNodeInfo#constants)

      ```java
      AccessibilityNodeInfo.performAction(AccessibilityNodeInfo.ACTION_CLICK);			//	点击
      AccessibilityNodeInfo.performAction(AccessibilityNodeInfo.ACTION_LONG_CLICK);		//	长按
      AccessibilityNodeInfo.performAction(AccessibilityNodeInfo.ACTION_FOCUS);			//	获取焦点
      AccessibilityNodeInfo.performAction(AccessibilityNodeInfo.ACTION_PASTE);			//	粘贴
          
      //	区分【android.accessibilityservice包】和【andorid.view.accessibility包】
      //	前者有【AccessibilityService()类】，后者有【AccessibilityEvent()类】和【AccessibilityNodeInfo()类】
      ```

6. :book:抢红包案例

   > [(31条消息) android 辅助功能（无障碍） AccessibilityService 实战入门详解_王能的小屋-CSDN博客_android 无障碍](https://blog.csdn.net/weimingjue/article/details/82744146)）

7. :book:【无障碍】参考

   > 指南书：[Android开发无障碍指南 (siaa.org.cn)](http://www.siaa.org.cn/static/image/img_media/Android无障碍开发指南.pdf)
   >
   > 名词解释：【[FLAG_INCLUDE_NOT_IMPORTANT_VIEWS](https://www.apiref.com/android-zh/android/accessibilityservice/AccessibilityServiceInfo.html#FLAG_INCLUDE_NOT_IMPORTANT_VIEWS)】和【[辅助功能 AccessibilityService笔记（2） - 简书 (jianshu.com)](https://www.jianshu.com/p/ef01ce654302)

8. demo分析

   ```java
   //	监听用户操作
   int eventType = event.getEventType();
   if (eventType == AccessibilityEvent.TYPE_VIEW_CLICKED) {			//	监听【鼠标点击】事件
   	Log.i(TAG, "触发鼠标点击事件...");
   } else if (eventType == AccessibilityEvent.TYPE_VIEW_TEXT_CHANGED) {
   	Log.i(TAG, "触发文字变化事件...");								//	监听【文字变化】事件
   }
   
   //	检索当前页面节点，并点击
   AccessibilityNodeInfo info = getRootInActivityWindow();
   List<AccessibilityNodeInfo> list = info.findAccessibilityNodesInfosByText("demo");			//	根据包含的关键字找到节点，可能有多个
   AccessibilityNodeInfo info = list.get(0);
   info.performAction(AccessibilityNodeInfo.ACTION_CLICK);									//	点击操作
   
   //	获取设备已经安装的APP包名——https://www.jianshu.com/p/22e223884d16
   PackageManager pm = getPackageManager();
   List<PackageInfo> list = pm.getInstalledPackages(PackageManager.GET_UNINSTALLED_PACKAGES);	//	获取包信息的List
   for (PackageInfo packageInfo : list) {
       String packageName = packageInfo.packageName;
       Log.d(TAG, "应用的包名：" + packageName);
   }
   ```


# 五、关于安卓项目（四大组件，五大布局，六大存储）

1. 安卓四大组件

   - 安卓项目结构和文件介绍：[(31条消息) Android—项目结构_xqy3177563的博客-CSDN博客_android项目结构](https://blog.csdn.net/xqy3177563/article/details/90142446)
   - 安卓生命周期和四大组件串联：[Android 四大组件 - 简书 (jianshu.com)](https://www.jianshu.com/p/51aaa65d5d25)
   - 安卓四大组件详解：[(31条消息) Android四大组件（整理相关知识点）_Calvert的博客-CSDN博客_安卓四大组件](https://blog.csdn.net/xchaha/article/details/80398620)
   - 关于Context详解：[Context详解 - jingmengxintang - 博客园 (cnblogs.com)](https://www.cnblogs.com/jingmengxintang/p/7889311.html)

2. 无障碍的几个类的总结

   - :snowflake:AccessibilityService类：用来继承，重写【连接】、【监听】和【中断】三大函数
   - getRootInActiveWindow()：获取窗口根节点，返回单个节点
   - performGlobalAction(action)：全局操作，无关当前环境
     1. GLOBAL_ACTION_HOME：home键
     2. GLOBAL_ACTION_BACK：back键
     3. GLOBAL_RECENTS：task键
   - AccessibilityServiceInfo类：用来【动态配置】权限/参数，以下为【静态配置】的XML文件
     1. accessibilityEventTypes：监听哪些变化，比如窗口打开，滑动等等
     2. accessibilityFeedbackType：反馈方式，比如语音，震动等等
     3. accessibilityFlags：应用获取哪些信息（[辅助功能 AccessibilityService笔记（2） - 简书 (jianshu.com)](https://www.jianshu.com/p/ef01ce654302)）
     4. canRequestFilterKeyEvents：请求过滤【KeyEvent】的属性，配合【flagRequestFilterKeyEvents】使用
     5. canRetrieveWindowContent：取回活动窗口的内容属性，配合【flagRetrieveInteractiveWindows】使用
     6. canPerformGestures：允许模拟手势的API实现
     7. description：简单描述无障碍
     8. notificationTimeout：两个辅助功能事件之间的最小间隔周期，一般设置100
   - :snowflake:AccessibilityEvent类：封装界面传递的事件信息
     1. getEventType()：事件类型
        - TYPE_NOTIFICATION_STATE_CHANGED：通知弹出
        - TYPE_WINDOW_STATE_CHANGED：dialog等用户界面变化
        - TYPE_WINDOW_CONTENT_CHANGED：基于当前【event.source】中的子节点的内容变化，或者说组件树变化
        - TYPE_WINDOWS_CHANGED：窗口的变化（不常用）
        - TYPE_VIEW_TEXT_CHANGED：界面文字改动事件
        - TYPE_VIEW_CLICKED：界面点击事件
     2. getSource()：获取事件源对应的节点信息
     3. getText()：获取事件源的文本信息
   - AccessibilityNodeInfo类：描述节点的类
     1. findAccessibilityNodeInfosByText(String)：通过【关键字】寻找节点，返回节点组成的【List】
     2. findAccessibilityNodeInfosByViewId(String)：通过【ID】寻找节点，返回节点组成的【List】
     3. performAction(action)：对节点进行操作
        - ACTION_CLICK：点击
        - ACTION_PASTE：粘贴
        - ACTION_SET_TEXT：填充文字

3. 【无障碍】相关参考文章

   - [详解安卓辅助功能服务AccessibilityService（无障碍服务，微信抢红包助手原理） - 简书 (jianshu.com)](https://www.jianshu.com/p/e1ba386464ad)
   - [(AccessibilityService) Android 辅助功能笔记 - 简书 (jianshu.com)](https://www.jianshu.com/p/959217070c87)
   - [(30条消息) android 辅助功能（无障碍） AccessibilityService 实战入门详解_王能的小屋-CSDN博客_安卓无障碍](https://blog.csdn.net/weimingjue/article/details/82744146)
   - [(30条消息) 深入了解AccessibilityService_Floating Cat-CSDN博客](https://lionoggo.blog.csdn.net/article/details/51794318?spm=1001.2101.3001.6650.15&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-16.no_search_link&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-16.no_search_link)

4. ## 【activity】和【context】关系

   - 【Context】是【Application】和【Activity】【Service】的基类；同时一个应用程序一般存在多个/两个【Context】，一个存在于当前【Activity】中，一个存在于整个应用程序中

     ```java
     Context context = this.getApplicationContext()	//	获取应用程序的Context
     Context context = Activity.this					//	获取当前Activity下的Context
     ```

   - Activity之间，通过【栈】的方式存储，即【Activity或者Dialog】通常建立在另一个Activity之上

     ```java
     //	参考文章：https://blog.csdn.net/u014665856/article/details/72354406
     //	注意区分：getApplicationContext()和getApplication()
     View.getContext()					//	返回当前View对象的Context
     Activity.this						//	返回当前Activity的实例
     Activity.getApplicationContext()	//	返回当前进程/全局下的Context，即把Application当作Context使用；生命周期是【整个应用】
     getApplication()					//	获取唯一的Application实例，即全局变量；存在于【Activity】或者【Service】中，生命周期是Activity
     ```

5. build.gradle初步学习

   - Gradle是基于Groovy的【领域特定语言/DSL】（注：DSL是帮助用户从某个系统中，抽象出部分功能或者简化某些操作的一种工具），用来声明项目设置并构建项目，而不是用原来的XML（注：ANT或者Maven，是基于XML的DSL）进行配置

   - 项目中一般出现2个或者多个，一个在【根目录】下，一个在【app目录】下；如果在【Android模式下】，则全部在【Gradle Scripts】文件下

   - 【根目录】下的【build.gradle】

     ```groovy
     buildscript {
         repositories {
             google()
             mavenCentral()			//	代码托管库，设置之后可以在项目中轻松引用该地址/库上的开源项目
         }
     
         dependencies {
             classpath 'com.android.tools.build:gradle:4.1.0'		//	声明了一个gradle插件
         }
     }
     ```

   - 【app目录】下的【build.gradle】

     ```groovy
     apply plugin: 'com.android.application'			//	声明该模块是Andorid应用，而不是库模块（注：库模块即com.android.library）
     apply from: "$flutterRoot/packages/flutter_tools/gradle/flutter.gradle"
     
     android {									//	配置项目各种属性，闭包
         compileSdkVersion 30					//	编译SDK的版本
         //	buildToolsVersion '26.0.2'				//	打包工具的版本号
     
         compileOptions {
             sourceCompatibility JavaVersion.VERSION_1_8
             targetCompatibility JavaVersion.VERSION_1_8
         }
     
         defaultConfig {							//	默认配置，闭包
             applicationId "com.example.get_android_version"	//	应用程序的包名（注：对应字段PackageName）
             minSdkVersion 17
             targetSdkVersion 30
             versionCode flutterVersionCode.toInteger()		//	版本号（注：此处版本号从【local.properties】文件获取），每次更新加一
             versionName flutterVersionName					//	版本名，显示给用户看到的版本号
         }
     
         buildTypes {							//	指定生成安装文件的配置，闭包
             release {							//	生成正式版安装文件的配置
                 // TODO: Add your own signing config for the release build.
                 // Signing with the debug keys for now, so `flutter run --release` works.
                 signingConfig signingConfigs.debug
             }
         }
     }
     
     flutter {
         source '../..'
     }
     
     dependencies {								//	指定当前项目的所有依赖关系，如：本地依赖，库依赖，远程依赖
         //	本地依赖，对本地Jar包货目录添加依赖关系	
         //	库依赖，对项目中的库模块添加依赖关系
         //	远程依赖，对远端库/地址上的开源项目添加依赖关系
         //	标准远程依赖格式：域名：组织名：版本名，如com.android.support:appcompat-v7:26.1.0
         implementation 'com.github.princekin-f:EasyFloat:2.0.3'
     }
     ```

   - 注：Android有两个标准的library文件服务器，一个是【jcenter】，另一个是【maven】，两者没有关系；jcenter有的maven可能没有，反之亦然

六、video_player组件

1. 简介：官方提供的播放视频的依赖/组件

2. 主要类

   ```dart
   //	VideoPlayer，视频【组件】，通过【VideoPlayerController】初始化
   VideoPlayer(_controller)
   //	VideoPlayerController，控制视频的实例对象，常用于加载视频源，视频的播放/暂停，以及相关事件监听
   VideoPlayerController _controller;
   //	VideoProgressIndicator，视频的进度条【组件】，通过【VideoPlayerController】初始化
   VideoProgressIndicator(_controller, allowScrubbing: true)
   ```

3. 情况（针对单个视频）

   - :snowflake:能够【https】和【http】请求资源
   - :snowflake:能够手动暂停/播放，设置加速播放，设置循环播放
   - :snowflake:能够展示进度条，拖拽播放
   - :question:横屏情况，展示有问题，可能是装视频的组件有问题
   - :question:多个视频的相关测试，情况未知

4. :book:参考信息

   > 库地址：[video_player | Flutter Package (pub.dev)](https://pub.dev/packages/video_player)
   >
   > 简单使用，以及三方组件的UI封装：[Flutter 视频播放 - 简书 (jianshu.com)](https://www.jianshu.com/p/caf7e3cd0df6)
   >
   > 网络权限配置，http网络请求：[(55条消息) Flutter视频播放、Flutter VideoPlayer 视频播放组件精要_早起的年轻人的博客-CSDN博客_flutter 视频播放](https://blog.csdn.net/zl18603543572/article/details/111327310)
   >
   > 进度条设置：[(54条消息) flutter video 支持拖动加载，单击可以暂停。_我来秋风扫落叶的博客-CSDN博客](https://blog.csdn.net/qq_15038701/article/details/97826132)
   >
   > 在线MP4视频资源：[MP4视频测试地址在线MP4文件 - 简书 (jianshu.com)](https://www.jianshu.com/p/34ce7f9b469a)

# 六、audioplayers组件

1. 简介

2. 主要方法

3. :book:参考信息

   > 库地址：[audioplayers | Flutter Package (pub.dev)](https://pub.dev/packages/audioplayers)
   >
   > 网络权限和http请求配置：[(55条消息) Flutter视频播放、Flutter VideoPlayer 视频播放组件精要_早起的年轻人的博客-CSDN博客_flutter 视频播放](https://blog.csdn.net/zl18603543572/article/details/111327310)
   >
   > 完整介绍和使用实现：[flutter -- 音频播放 audioplayers - 简书 (jianshu.com)](https://www.jianshu.com/p/288f869690f0)

# 附录

1. :snowflake:快捷键
   - Alt+Ctrl+L：格式化代码
   
2. 在线MP4资源：[MP4视频测试地址在线MP4文件 - 简书 (jianshu.com)](https://www.jianshu.com/p/34ce7f9b469a)

3. :snowflake:参考书

   > 《Flutter实战-第二版》：https://book.flutterchina.club/chapter3/img_and_icon.html
   >
   > flutter_swiper插件：[flutter_swiper | Flutter Package (flutter-io.cn)](https://pub.flutter-io.cn/packages/flutter_swiper)

# 问题

- 访问阿帕奇仓库失败

  :snowflake:最新的国内镜像网站：[(16条消息) package命令报错Connect to repo.maven.apache.org:443 [repo.maven.apache.org/151.101.52.215\]_→_→BéLieve的博客-CSDN博客](https://blog.csdn.net/weixin_46099269/article/details/107665484)

  :snowflake:阿里云Maven镜像：[仓库服务 (aliyun.com)](https://developer.aliyun.com/mvn/guide)

  :snowflake:配置方式：[Could not resolve all artifacts for configuration ':classpath'. - 谜语+ - 博客园 (cnblogs.com)](https://www.cnblogs.com/022414ls/p/13469136.html)

  :snowflake:gradle理解：[(16条消息) 【Android】解决Kotlin依赖无法下载的问题_midnight_time的博客-CSDN博客](https://blog.csdn.net/midnight_time/article/details/104449443)



