# 符号注释

- :book:注释
- :snowflake:一般分类
- :question:问题
- :cherry_blossom:其他分类

# 一、环境配置与安装

1. 设置国内镜像源，下载SDK：[(28条消息) Flutter的环境搭建和配置_smxueer的专栏-CSDN博客_flutter环境配置](https://blog.csdn.net/smxueer/article/details/82051118?ops_request_misc=&request_id=&biz_id=102&utm_term=flutter网络环境配置&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-5-82051118.pc_search_all_es&spm=1018.2226.3001.4187)
   - cmd中，输入第一句：set PUB_HOSTED_URL=https://pub.flutter-io.cn
   - cmd中，输入第二句：set FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
   - 克隆SDK文件：git clone https://github.com/flutter/flutter.git -b stable
     - 出现【unable to access 'https://...'】的问题，关闭代理：git config --global --unset https.proxy（[(28条消息) 完美解决 fatal: unable to access 'https://github.com/.../.git': Could not resolve host: github.com_桃九醉的博客-CSDN博客](https://blog.csdn.net/qq_38415505/article/details/83687207)）
2. 设置path环境变量，重启所有命令行窗口，包括VS Code，再运行【flutter doctor】：[1. 安装和环境配置 - Windows - 《Flutter 1.12 官方开发文档》 - 书栈网 · BookStack](https://www.bookstack.cn/read/flutter-1.2-zh/c02f8b2ba3dcc1ae.md)
   - 设置【用户变量】中的【path】：C:\Users\Aijiar\Desktop\flutter\bin
   - 运行【flutter doctor】：当开发者们从 GitHub 安装（而不是从预打包的归档文件中安装），为了要执行 `flutter` 命令，Flutter 工具将会在首次运行时从谷歌服务器下载 Dart SDK。升级 Flutter 时亦会发生 (比如运行 `flutter upgrade` 命令) 
   - ![image-20211020111229527](C:\Users\zyc\AppData\Roaming\Typora\typora-user-images\image-20211020111229527.png)
   - 安装【Android Studio】和【Android SDK】：【[(28条消息) Android Studio安装配置详细步骤（超详细）_『愚』的博客-CSDN博客_android studio安装](https://keafmd.blog.csdn.net/article/details/108942788)】和【[(28条消息) cmdline-tools component is missing_吃饭了吗的博客-CSDN博客](https://blog.csdn.net/weixin_41824429/article/details/118942087?ops_request_misc=&request_id=&biz_id=&utm_medium=distribute.pc_search_result.none-task-blog-2~all~es_rank~default-1-118942087.pc_search_all_es&utm_term=cmdline-tools+component+is+mis&spm=1018.2226.3001.4187)】
3. 安装【VS Code】以及对应的插件：（[Flutter 中文文档 - Flutter 中文资源 | 编辑工具设定](https://flutter.cn/docs/get-started/editor?tab=vscode)）
   - 安装【Dart】和【Flutter】插件
   - 打开【查看】——【命令面板】，输入【doctor】，选择【Flutter: Run Flutter Doctor】，查看输出
4. 通过模板，实现Demo
   - 注意：文件名最好使用【my_app】形式（[dart/flutter 中的代码规范 - 简书 (jianshu.com)](https://www.jianshu.com/p/047eb78dce53)）

# 二、Flutter知识

1. 参考文章：[(28条消息) Flutter常用命令行_大灰狼的小绵羊哥哥的博客-CSDN博客_flutter 命令](https://blog.csdn.net/sinat_17775997/article/details/106418282)

2. 常用指令

   ```dart
   flutter run			//	运行项目
   flutter pub get		//	获取依赖项
   ```
   
3. 生命周期：[[Flutter\] 10-Flutter的生命周期 - 简书 (jianshu.com)](https://www.jianshu.com/p/6ed6f7de01ff)

# 三、第三方插件库

1. 参考文章：[Flutter第三方插件汇总（持续更新） - 掘金 (juejin.cn)](https://juejin.cn/post/6874082988381241357#heading-20)

# 四、Packages的开发和提交

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

   

# 五、无障碍服务

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


# 六、关于安卓项目（四大组件，五大布局，六大存储）

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

# 附录

1. :cherry_blossom:快捷键
  - Alt+Ctrl+L：格式化代码

