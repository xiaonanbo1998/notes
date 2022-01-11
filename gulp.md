# Gulp-自动化构建工具

1. 入门与初始化运行

   - 安装【gulp】，查看【版本号】
   - 运行【gulp】文件

2. 基础了解

   - Node 的模块解析功能允许你将 `gulpfile.js`' 文件替换为同样命名为 `gulpfile.js` 的目录，该目录中包含了一个名为 `index.js` 的文件，该文件被当作 `gulpfile.js` 使用。并且，该目录中还可以包含各个独立的任务（task）模块。

   - 导出【任务/Task】，和引入

     ```javascript
     exports.build = build;					//	导出【公有任务】
     exports.default = series(clean, build);
     
     const { series } = require('gulp')		//	引入模块
     ```

   - 组合任务

     1. 顺序任务：series(fn1[, fn2, ...])
     2. 并发任务：parallel(fn1[, fn2, ...])

   - 异步任务，通常需要引入相应【js文件】

     1. 比如【stream】、【promise】、【event emitter】、【child process】等等

     2. > [异步执行 · gulp.js 中文文档 (gulpjs.com.cn)](https://www.gulpjs.com.cn/docs/getting-started/async-completion/)

3. 处理文件

   - :pineapple:src()函数：读取文件
   - :pineapple:pipe()函数：发出【异步完成】信号
   - :pineapple:dest()函数：输出文件
   - :pineapple:uglify()函数：压缩混淆文件

4. glob解释

   - 本质是字符串，用于匹配文件路径
   - 字符串片段/segment是【两个分隔符之间的字符串】，分隔符是【/】，转义符是【\\】
   - 特殊字符——【*】
   - 特殊字符——【**】
   - :question:特殊字符——【!】

5. 插件和模块

   - 模块，条件插件，内联插件等等

   - > [使用插件 · gulp.js 中文文档 (gulpjs.com.cn)](https://www.gulpjs.com.cn/docs/getting-started/using-plugins/)

6. 文件监控

> [JavaScript 和 Gulpfile · gulp.js 中文文档 (gulpjs.com.cn)](https://www.gulpjs.com.cn/docs/getting-started/javascript-and-gulpfiles/)

# 参考文档

> 内容替换：[gulp常用插件之gulp-replace使用 - 较瘦 - 博客园 (cnblogs.com)](https://www.cnblogs.com/jiaoshou/p/12184941.html)
>
> 本地文件打包、处理的综合版本：[gulp自动化构建（css、js文件压缩以及版本修改） - 简书 (jianshu.com)](https://www.jianshu.com/p/a37457cfbf3f)
>
> 文件引入：[使用 gulp 搭建前端环境之CommonJs & ES6 模块化(中级篇) - sunshine1987 - 博客园 (cnblogs.com)](https://www.cnblogs.com/lidongyue/articles/5269755.html)

- 插件：[利用Gulp实现前端打包自动上传服务器 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1653701)
- 插件：[gulp gulp-sftp 上传服务器 - 简书 (jianshu.com)](https://www.jianshu.com/p/cbbfccfde747)