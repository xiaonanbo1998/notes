# Gulp-自动化构建工具

1. 检查环境，安装【命令行工具】

   ```shell
   node --version			//	node版本
   npm --version			//	npm版本
   npx --version			//	npx版本
   
   npm install --global gulp-cli		//	命令行工具
   ```

2. 试运行

   - 创建目录，安装开发依赖

   ```shell
   npx mkdirp gulp-project	//	创建【gulp-project】目录
   cd gulp-project
   npm init			//	创建项目，配置相关参数
   npm install --save-dev gulp			//	安装开发依赖【gulp】
   gulp --version		//	检查版本
   //	结果，仅参考
   CLI version 2.0.1
   Local version 4.0.0
   ```

   - 创建【gulpfile.js】文件

   ```javascript
   function defaultTask(cb) {	//	cb变量，函数作为【任务】的时候不用传入，单独调用不传参会报错
       //	other codes
       cb()
   }
   exports.default = defaultTask	//	【default】是【直接】执行【gulp】指令时，默认启动的【task】
   exports.other = defaultTask		//	【other】是自定义【task】，可选择执行
   ```

   - 测试

   ```shell
   gulp					//	等于【gulp default】
   gulp task1 task2		//	执行task1和task2
   ```

   - :notebook_with_decorative_cover:Node 的模块解析功能允许你将 `gulpfile.js`' 文件替换为同样命名为 `gulpfile.js` 的目录，该目录中包含了一个名为 `index.js` 的文件，该文件被当作 `gulpfile.js` 使用。并且，该目录中还可以包含各个独立的任务（task）模块。

3. 基础API，模块和插件

   - 项目一定要有【gulpfile.js】文件或者【gulpfile.js文件夹】和文件夹下的【index.js】文件
   - 常用API
     - :pineapple:src()函数：文件读取
     - :pineapple:dest()函数：文件输出
     - :pineapple:series()函数：串行任务
     - :pineapple:parallel()函数：并发任务
     - :pineapple:pipe()函数：发出【异步完成】信号
     - :pineapple:uglify()函数：压缩混淆文件
   - 常用模块：【gulp-rename】、【gulp-replace】、【fs】、【path】
   - 插件：【gulp-ssh】、【gulp-sftp】、【cos-nodejs-sdk-v5】

4. CommonJs的模块化语法

   ```shell
   //	主要的使用方式
   //	file1.js
   function eat() {
   	console.log('wanna eat hamburger...')
   }
   module.exports.eat = eat
   
   //	file2.js
   const action = require('./file1')
   action.eat()
   ```

   > 参考：【干饭人】——【二十一、CommonJS和NodeJS模块化】

5. 常用指令

   - gulp：执行【default任务】
   - gulp --version：查看版本号
   - gulp --tasks：查看注册的【task/任务】
   - gulp taskName：执行【taskName】任务

6. 参考网址

   > gulp网址：[JavaScript 和 Gulpfile · gulp.js 中文文档 (gulpjs.com.cn)](https://www.gulpjs.com.cn/docs/getting-started/javascript-and-gulpfiles/)
   >
   > COS网址：[腾讯云-控制台 (tencent.com)](https://console.cloud.tencent.com/cos5/bucket?bucket=coffee-1309193918&region=ap-chengdu)
   >
   > 内容替换：[gulp常用插件之gulp-replace使用 - 较瘦 - 博客园 (cnblogs.com)](https://www.cnblogs.com/jiaoshou/p/12184941.html)
   >
   > 本地文件打包、处理的综合版本：[gulp自动化构建（css、js文件压缩以及版本修改） - 简书 (jianshu.com)](https://www.jianshu.com/p/a37457cfbf3f)
   >
   > 文件引入：[使用 gulp 搭建前端环境之CommonJs & ES6 模块化(中级篇) - sunshine1987 - 博客园 (cnblogs.com)](https://www.cnblogs.com/lidongyue/articles/5269755.html)
   >
   > 插件：[利用Gulp实现前端打包自动上传服务器 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1653701)
   >
   > 插件：[gulp gulp-sftp 上传服务器 - 简书 (jianshu.com)](https://www.jianshu.com/p/cbbfccfde747)
