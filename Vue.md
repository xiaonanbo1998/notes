# 一、Vue Router

1. :whale:基础使用

   ```html
   <!-- 导航，渲染成a标签，to属性指定链接🔗 -->
   <router-link to="/foo">Go to Foo</router-link>
   <!-- 页面，渲染的页面/组件✌ -->
   <router-view></router-view>
   ```

   ```javascript
   //	写法一
   const Foo = { template: '<div>foo</div>'}		//	1、定义【路由组件】
   const routes = [								//	2、定义【路由】
       {path: '/foo', component: Foo}
   ]
   const router = new VueRouter({					//	3、创建【router实例】并配置
       routes									//	缩写：routes: routes
   })
   const app = new Vue({						//	4、通过【router】属性注入路由，同时创建和挂载根实例
       router
   }).$mount('#app')
   
   
   //	写法二
   const foo = () => import('@/pages/foo')			//	foo.vue文件
   const router = new VueRouter({
       routes: [
           {path: '/foo', component: foo}
       ]
   })
   export default router
   import router from './router'
   new Vue({
       el: '#app',
       router
   })
   ```

   - :warning:通过【this.$router】访问路由器，通过【this.$route】访问当前路由

   - :book:参考

     > [起步 | Vue Router (vuejs.org)](https://router.vuejs.org/zh/guide/)

2. :whale:简单的动态路由匹配

   ```javascript
   import foo = () => import('@/pages/foo')
   const router = new VueRouter({
       routes: [
           {path: '/foo/:id', component: foo}			//	则【/foo/userone】和【/foo/usertwo】都映射到相同路由
       ]
   })
   ```

   - :warning:通过【this.$route.params.id】获取传入参数

   - :warning:组件复用，不会再触发组件的【生命周期函数】

   - :book:参考

     > [动态路由匹配 | Vue Router (vuejs.org)](https://router.vuejs.org/zh/guide/essentials/dynamic-matching.html)

3. :whale:嵌套路由

   - :warning:注意以【/】开头的【根路径】

   - 访问【有子路由的根路由】时，界面不会有任何东西，必须匹配子路由

   - :book:参考

     > [嵌套路由 | Vue Router (vuejs.org)](https://router.vuejs.org/zh/guide/essentials/nested-routes.html)

4. :whale:编程式导航

   ```javascript
   //	this.$router.push()，声明式【<router-link :to="...">】，入栈操作
   // 字符串
   this.$router.push('home')
   
   // 对象
   this.$router.push({ path: 'home' })
   
   // 命名的路由
   this.$router.push({ name: 'user', params: { userId: '123' }})
   
   // 带查询参数，变成 /register?plan=private
   this.$router.push({ path: 'register', query: { plan: 'private' }})
   
   
   //	this.$router.replace()，声明式【<router-link :to="..." replace>】，替换栈顶
   
   
   //	this.$router.go(num)，history栈中向前或者向后多少步
   ```

5. :whale:命名路由和:whale:命名视图

   ```javascript
   //	命名路由
   const router = new VueRouter({
       routes: [
           {
               path: '/user/:userId',
               name: 'user',
               component: User
           }
       ]
   })
   
   //	命名视图
   //	路由组件一【router-view/】，默认名称【default】
   //	路由组件二【router-ciew name="two"】
   const router = new VueRouter({
       routes: [
           {
               path: '/',
               components: {			//	注意是【components】，多了一个s
                   default: Foo,
                   two: Bar
               }
           }
       ]
   })
   ```

6. :whale:重定向和别名

   ```javascript
   const router = new VueRouter({
       routes: [
           {
               path: '/a',
               redirect: '/b'					//	写法一
           },
           {
               path: '/c',
               redirect: {name: 'ddd'}			//	写法二
           }
       ]
   })
   ```

7. :whale:路由组件传参？？？？？？？？？？？？？？？？？？

# 二、例子

1. 项目结构

   ```markdown
   - build     ---- vue和webpack的配置目录(不用管)
   - config    ---- vue编译配置目录(不用管)
   - node_modules  ----安装的模块目录(不用管, 该目录不能上传到SVN或者GIT)
   - src   ---- 开发源码目录
       -- assets   ---- 资源存放目录
       -- components   ---- 组件存放目录
       -- config       ---- 项目配置目录
       -- mixins       ---- mixin存放目录
       -- pages        ---- 页面存放目录
       -- plugins      ---- vue插件存放目录
       -- router       ---- 路由存放目录
       -- service      ---- 跟后端交互的存放目录
       -- store        ---- vuex状态管理目录
       -- utils        ---- 工具类存放目录
       -- App.vue      ---- vue入口，即填充【index.html】页面的Vue页面
       -- main.js      ---- main函数，初始化Vue页面，加载vuex，加载router等等
       -- element-variables.scss   ---- element-ui样式管理入口
   - static        ---- 静态资源目录(不用管)
   - .svnignore    ---- svn忽略配置文件，文件里配置的内容都不要提交上传到SVN
   - .gitignore    ---- svn忽略配置文件，文件里配置的内容都不要提交上传到GIT
   - index.html    ---- 整个项目的入口，即【网页的首页】
   - package.json  ---- 模块依赖管理配置文件，包括【开发依赖】、【运行依赖】、【调试/运行】
   - yarn-error.log    ---- yarn报错日志，不要提交上传到SVN或GIT
   - yarn.lock         ---- yarn配置文件，非必须，根据package.json执行yarn后生成
   ```

2. 分层结构：页面——业务——服务/插件——工具/资源

3. 补充学习

   - ——————————————————分割线（main.js部分）——————————————————————

   - module.exports：

   - import的使用

     ```javascript
     import Vue from 'vue'	//	引入Vue框架内置vue文件，调用方式是【类名Vue】（注：axios、Vuex同样适用）
     import App from './App'	//	引入当前文件根目录下的【App.vue】文件，将暴露的对象通过【类名App】来调用（注：vue文件可以省略【.vue】后缀）
     import router from './router'	//	引入当前文件根目录下【router】文件夹中的【index.js】文件(注：store()同样适用)
     import './plugins/element.js'	//	直接引入【element.js】文件
     import mixins from './mixins/my-mixin'	//	引入【my-mixin.js】文件（注：js文件可以省略【.js】后缀）
     import { MessageBox } from 'element-ui'	//	引入【element-ui】中的部分组件
     ```

   - Vue.use(myPlugin)

   - Vue.mixin(mixins)

   - new Vue的使用

     ```vue
     new Vue({
       el: '#app',
       data () {
         return {
           eventHub: new Vue()
         }
       },
       router,
       store,
       components: { App },
       template: '<App/>'
     })
     ```

   - ——————————————————分割线（路由部分）——————————————————————

   - 【router-view】的使用，以及

     ```javascript
     const Layout = () => import('@/pages/layout')		//	预加载？？？；@指代【./src】路径
     //	初始化VueRouter的操作，比如scrollBehavior方法/属性，mode属性，routes属性
     export default router							//	向外暴露【router】对象
     ```

   - 参考官网：[Vue Router (vuejs.org)](https://router.vuejs.org/zh/)

   - ——————————————————分割线（插件部分）——————————————————————

   - element-ui插件，版本信息生成插件

   - 自主实现的插件【my-plugins.js】，调用工具类【my-utils.js】

     ```javascript
     const myPlugin = {
     	install (Vue) {				//	install() {}？？？
     		console.log('开始装载自定义插件功能.')
     		Vue.prototype.$dayjs = myUtil.$dayjs
     		Vue.prototype.$debounce = myUtil.debounce
     		Vue.prototype.downloadFile = myUtil.downloadFile
     	}
     }
     function debounce() {}			//	防抖函数，作用？？？
     function setStorage() {}		//	封装的持久化存储
     function getStorage() {}		//	封装的获取持久化存储数据的函数
     function throttle() {}			//	节流函数，作用？？？
     function downloadFile() {}		//	封装的下载文件函数（有点眼熟Ajax）
     ```

   - ——————————————————分割线（Vuex部分）——————————————————————

   - Vuex的三个组成部分（state、mutation、action）

     ```javascript
     Vue.use(Vuex)						//	通过use()函数注入？？？
     export default new Vuex.Store({		//	通过【Vuex.Store()】初始化
         state,							//	定义需要管理的变量，调用变量的【两种方式】
         mutations,						//	通过Vuex同步修改变量，调用函数的【两种方式】
         actions							//	通过Vuex异步修改变量，调用函数的【两种方式】
     })
     ```

   - ——————————————————分割线（mixin部分）——————————————————————

   - 了解概念

   - ——————————————————分割线（service部分）——————————————————————

   - 【sessionStorage】和【localStorage】区别和使用

   - 【Promise类】的使用

# 三、其他

1. 命名规则
   
   - 组件：【current-button】
   - 文件：【serviceManagement】
   
2. 对象存储

   - 概述：COS（注：【腾讯云】提供的存储海量文件的分布式存储服务），OSS（注：【阿里云】提供的海量、高可靠的云存储服务）和OBS（注：【华为云】存储服务）等等，都是将存储数据当作对象单独对待，尽管数据可能是非结构化的扁平层级数据。
   - 优势：各个终端可直接向OSS写入或者读取数据，同时配合【原生的传输加速功能】，【CDN产品】，提升重复且并发的下载体验
   - 对比【云盘】：容量提升（注：超大规模机群）；安全性提升（注：冗余备份等等）等等

3. ES2017的【async】和【await】

   - 【async】让函数成为【异步函数】，返回Promise（注：Promise有【catch()函数】、【then()函数】以及【all()函数】）

   - Promise内部，正常执行的是【Promise.resolve()函数】，异常则执行【Promise.reject()函数】

   - 【await】关键字，只能在【async】表明的异步函数中使用

     ```javascript
     function testAsy(x){
        return new Promise(resolve=>{setTimeout(() => {
            resolve(x);
          }, 3000)
         }
        )
     }
     async function testAwt(){    
       let result =  await testAsy('hello world');
       console.log(result);    // 3秒钟之后出现hello world
       console.log('tangj')   // 3秒钟之后出现tangj
     }
     testAwt();
     console.log('tangSir')  //立即输出tangSir
     ```

4. [从vue源码解析Vue.set()和this.$set()_vue.js_脚本之家 (jb51.net)](https://www.jb51.net/article/146580.htm)

# 四、模块导入

1. 用法一

   ```javascript
   //	file1.js
   let obj = {name: 'hank'}
   export default obj1
   
   //	file2.js
   import obj from './file1'
   console.log(obj.name)
   ```

2. 用法二

   ```javascript
   // file1.js
   export let str = 'hank'
   export let num = 1
   
   //	file2.js
   import {str, num} from './file1.js'
   console.log(str)
   
   //	file3.js
   import * as obj from './file1.js'
   console.log(obj.str)
   ```

3. 用法三

   ```javascript
   //	file1.js
   console.log('hello')
   
   //	file2.js
   import './file1.js'
   //	打印得到【hello】
   ```

   
