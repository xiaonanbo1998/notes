# 一、常用指令

​	

```
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

# 二、附录

1. 参考文章：[Yarn vs npm：你需要知道的一切 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/23493436#:~:text=npm install 命令安装的是 package.json 中的依赖，如果开发者在 package.json 中添加了新的依赖，npm install,也一样安装。 然而，yarn install 会优先安装 yarn.lock 中记录的依赖，没有这样的锁定文件时，才会去安装 package.json 中的依赖。)

