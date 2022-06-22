# 零、表情符号

- :lemon:一般分类
- :book:参考

# 一、基础理解

1. yarn和npm，两者都是对【Node.js】运行环境中【包/模块/依赖】的管理

2. 【Node.js】是运行在服务端的JS（环境）

3. 版本验证

   ```bash
   #	node版本
   node -v
   #	npm版本
   npm -v
   #	当前目录依赖，ls = list
   npm ls --dept 0
   #	全局依赖
   npm ls -g --dept 0
   #	查看具体某项依赖
   npm ls <packagename> [--dept 0]
   ```
   
4. :book:参考

   > 查看依赖：[npm查看全局安装过哪些包(插件)_03251108的技术博客_51CTO博客](https://blog.51cto.com/u_11871779/2287392)

# 二、常用指令

```shell
#	安装
npm install			#	by default, [npm install] will install all modules listed as dependencies in [package.json]
npm install			#	this saves any specified packages into [dependencies] by default
-S == --save		#	package will appear in [dependencies]
-D == --save-dev	#	package will appear in [devDependencies]
-g == --global		#	package will be installed globally rather than locally
npm install == npm i	# abbreviation
npm run start == npm start	# abbreviation

#	更新
npm update			#	all packages in the specified location(global or local) will be updated
npm update -g		#	this will update globally installed packages

yarn help			#	access the list of commands
yarn || yarn install	#	install all the dependencies
yarn upgrade [package]	#	upgrade package to the latest version and update [package.json]
```

# 三、关于package.json

1. 了解：一个记录文件，管理npm依赖包

2. 创建方式

   ```shell
   npm init		//	创建文件，需要手动配置一些参数
   npm init -y
   npm init --yes	//	同上，自动创建文件，参数默认
   
   npm set init.author.email "wombat@npmjs.com"			//	手动设置初始化参数
   ```

   - :book:tips：如果文件中中没有描述字段，package.json就会使用【README.md】的第一行。该描述可帮助人们在搜索npm时找到您的包，因此在package.json中写入自定义描述，可以让人更容易找到包。

3. 两种类型的【依赖包列表】

   - dependencies：项目生产环境中需要的包

   - devDependencies：开发和测试中需要的包

     ```json
     {
       "name": "my_package",
       "version": "1.0.0",
       "dependencies": {
         "my_dep": "^1.0.0"
       },
       "devDependencies" : {
         "my_test_framework": "^3.1.0"
       }
     }
     ```

   - 安装方式

     ```shell
     npm install packageName --save		//	添加到dependencies，或者是--saveDev
     npm install packageName -S			//	abbreviation
     npm install packageName --save-dev	//	添加到devDependencies
     npm install packageName -D			//	abbreviation
     
     npm i moduleName					//	安装模块到项目目录下（dependencies节点中）
     npm i install -g moduleName			//	安装模块到全局，npm config prefix查看
     ```

     :lemon:npm i moduleName
     - 安装模块到【node_modules】目录下
     - 将模块依赖写入【dependencies】节点中
     - 运行【npm i】初始化项目时，会下载模块
     - 运行【npm i --production】或者注明【NODE_ENV】值为【production】时，会自动下载模块
     
     :lemon:npm i -g moduleName
     - 全局安装，不会在【node_modules】目录下
     - 不会将模块依赖写入两个节点
     - 运行【npm i】初始化项目时，不会下载模块
     
     :lemon:npm i --save moduleName
     - 安装模块在【node_modules】目录下
     - 模块依赖写入【dependencies】节点
     - 运行【npm i】初始化项目时，会下载模块
     - 运行【npm i --production】或者注明【NODE_ENV】值为【production】时，会自动下载模块
     
     :lemon:npm i --save-dev moduleName
     - 安装模块在【node_modules】目录下
     - 模块依赖写入【devDependencies】节点
     - 运行【npm i】初始化项目时，会下载模块
     - 运行【npm i --production】或者注明【NODE_ENV】值为【production】时，不会自动下载模块
     
   - :book:参考

     > 关于package.json：[npm关于package.json安装的那些事 - SegmentFault 思否](https://segmentfault.com/a/1190000017552119)
     >
     > JavaScript学习指南（第三版）

4. 依赖的版本管理

   - ~0.13.0：只更新补丁版本，即0.13.1可以，0.14.0不可以

   - ^0.13.0：更新补丁和次版本，即0.13.1可以，0.14.0可以

   - 0.13.0：只更新确切版本

5. :lemon:package-lock.json文件

   - 作用：考虑到部分依赖是通过【~或^】来指定，在另一台机器上面【npm i】初始化项目的时候，同样的项目，依赖实际上是不同的。该文件则会固化每个依赖的确切版本，初始化的时候，会指定确切版本。此外，执行【npm update】时，该文件中的依赖版本会更新

   - :book:参考

      > 是否写入.gitignore：[聊聊 package-lock.json 那些事儿 - 掘金 (juejin.cn)](https://juejin.cn/post/7000179306764714020)


# 附录

> yarn和npm对比：[Yarn vs npm：你需要知道的一切 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/23493436#:~:text=npm install 命令安装的是 package.json 中的依赖，如果开发者在 package.json 中添加了新的依赖，npm install,也一样安装。 然而，yarn install 会优先安装 yarn.lock 中记录的依赖，没有这样的锁定文件时，才会去安装 package.json 中的依赖。)
>
> yarn文档：[3 - 用法 | Yarn - JavaScript 软件包管理器 | Yarn 中文文档 - Yarn 中文网 (yarnpkg.cn)](https://www.yarnpkg.cn/getting-started/usage)
