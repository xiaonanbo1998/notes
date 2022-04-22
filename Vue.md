# 零、表情符号

- :whale:一级类别
- :warning:注意
- :ice_cream:【小知识点】下的类别
- :book:参考

# 一、Vue Router

1. 基础使用

   ```html
   <!-- 导航，渲染成a标签，to属性指定链接🔗 -->
   <router-link to="/foo">Go to Foo</router-link>
   <!-- 页面，渲染的页面/组件✌ -->
   <router-view></router-view>
   ```

   ```javascript
   //	写法一
   const Foo = { template: '<div>foo</div>' }			//	1、定义【路由组件】
   const routes = [								//	2、定义【路由】
       {path: '/foo', component: Foo}
   ]
   const router = new VueRouter({					//	3、创建【router实例】并配置
       routes
   })
   const app = new Vue({							//	4、通过【router】属性注入路由，同时【创建和挂载】根实例
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

   - :warning:通过【this.$router】访问【路由器】，通过【this.$route】访问【当前路由】

   - :book:参考

     > [起步 | Vue Router (vuejs.org)](https://router.vuejs.org/zh/guide/)

2. :whale:动态路由匹配

   ```javascript
   import foo = () => import('@/pages/foo')
   const router = new VueRouter({
       routes: [
           {path: '/foo/:id', component: foo}			//	则【/foo/userone】和【/foo/usertwo】都映射到相同路由
       ]
   })
   ```

   - :warning:动态路径参数，以冒号开头，如【/foo/:id】，参数值设置到【this.$route.params】对象中

   - :warning:组件复用，不会再触发组件的【生命周期函数】，可以通过【watch属性】监听【$route】对象的变化

     ```javascript
     const User = {
         template: '...',
         watch: {									//	方法一
             $route(to, from) {
                 //	对路由变化的响应
             }
         },
         beforeRouteUpdate(to, from, next) {				//	方法二，导航守卫
             //	react to route changes...
             next()
         }
     }
     ```

   - 匹配优先级：同一个路径匹配多个路由的时候，优先级为【路由的定义顺序，从前到后，优先级递减】

   - :book:参考

     > [动态路由匹配 | Vue Router (vuejs.org)](https://router.vuejs.org/zh/guide/essentials/dynamic-matching.html)

3. :whale:嵌套路由

   - 案例

      ```html
      <div id="app">
          <router-view></router-view>				<!-- 顶层出口 -->
      </div>
      ```

      ```vue
      const User = {
      	template: `
      		<div class="user">
                  <h2>User {{ $route.params.id }}</h2>
                  <router-view></router-view>
      		</div>`
      }
      ```

      ```javascript
      const router = new VueRouter({
          routes: [
              {
                  path: '/user/:id',
                  component: User,
                  children: [							//		嵌套路由的关键配置
                      path: 'profile',				//		没有【/】符号，匹配【/user/:id/profile】路径
                      component: UserProfile
                  ]
              }
          ]
      })
      ```

4. :whale:编程式导航

   - :warning:注意【/】的使用

   ```javascript
   //	编程式【this.$router.push()】，声明式【<router-link :to="...">】，入栈操作
   //	字符串
   this.$router.push('home')
   
   //	对象
   this.$router.push({ path: 'home' })
   
   //	命名的路由，变成 /user/123，注意是【name】不是【path】
   this.$router.push({ name: 'user', params: { userId: '123' }})
   //	等价于
   const userId = '123'
   this.$router.push({ path: `/user/${userId}` })
   
   //	带查询参数，变成 /register?plan=private
   this.$router.push({ path: 'register', query: { plan: 'private' }})
   
   //	this.$router.replace(location, onComplete?, onAbort?)，声明式【<router-link :to="..." replace>】，替换栈顶
   
   //	this.$router.go(num)，history栈中向前或者向后多少步
   ```

   - :book:参考

     > [编程式的导航 | Vue Router (vuejs.org)](https://v3.router.vuejs.org/zh/guide/essentials/navigation.html)

5. :whale:【命名路由】和【命名视图】

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
   //	声明式导航【<router-link :to="{ name: 'user', params: { userId: 123 }}">】
   //	编程式导航【this.$router.push({ name: 'user', params: { userId: 123 }})】
   
   
   //	命名视图
   //	路由组件一【router-view/】，默认名称【default】
   //	路由组件二【router-view name="two"】
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

   - :book::warning:参考案例：嵌套命名视图

     > [命名视图 | Vue Router (vuejs.org)](https://v3.router.vuejs.org/zh/guide/essentials/named-views.html#嵌套命名视图)

6. :whale:重定向和别名

   ```javascript
   //	重定向
   const router = new VueRouter({
       routes: [
           {
               path: '/a',
               redirect: '/b'					//	写法一，字符串
           },
           {
               path: '/a',
               redirect: {name: 'foo'}			//	写法二，对象
           },
           {
               path: '/a',
               redirect: to => {
                   //	方法接收【目标路由】作为参数，这里即【/a】
                   return  '' || {}			//	返回【字符串路径】或者【路径对象】
               }
           }
       ]
   })
   
   //	别名
   const router = new VueRouter({
       routes: [
           {
               path: '/a',
               component: A,
               alias: '/b'
           }
       ]
   })
   ```

7. 路由组件传参？？？？？？？？？？？？？？？？？？

8. VueRouter模式

   - 默认【hash模式】

   - 可选【history模式】等等

     ```javascript
     const router = new VueRouter({
         mode: 'history',
         routes: [...]
     })
     ```

9. 进阶

   :ice_cream:导航守卫，:book:参考

   > [导航守卫 | Vue Router (vuejs.org)](https://v3.router.vuejs.org/zh/guide/advanced/navigation-guards.html#完整的导航解析流程)

   :ice_cream:路由懒加载，:book:参考

   > [路由懒加载 | Vue Router (vuejs.org)](https://v3.router.vuejs.org/zh/guide/advanced/lazy-loading.html#路由懒加载)

   :ice_cream:导航故障，:book:参考

   > [导航故障 | Vue Router (vuejs.org)](https://v3.router.vuejs.org/zh/guide/advanced/navigation-failures.html#导航故障)

10. 案例

    - 监听【route】

      ```javascript
      watch: {
          $route (to, from) {							//	方法一
              console.log(to.path)
          },
      	$route: {									//	方法二
              handler: function (val, oldVal) {
                  console.log(val)
              },
              //	深度观察监听
      		deep: true
          }
      }
      ```

      :book:参考

      > [Vue监听路由变化 - 简书 (jianshu.com)](https://www.jianshu.com/p/c0440894c82e)

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


# 五、Vuex

1. 【状态/state】和【全局对象】

   - Vuex状态存储是【响应式】的，状态/state变化，相应组件也高效更新
   - 不能【直接改变/赋值】等操作状态/state，唯一途径是【显式提交/commit】一个mutation，能跟踪状态变化的前后，方便工具调试

2. 基础操作

   - 初始化

     ```javascript
     import Vue from 'vue'
     import Vuex from 'vuex'
     
     Vue.use(Vuex)
     
     const store = new Vuex.Store({
         state: {
             count: 0,
         },
         mutations: {
             increment (state) {
                 state.count++
             }
         }
     })
     ```

   - 直接调用

     ```javascript
     store.commit('increment')
     console.log(store.state.count)			//	结果是【1】
     ```

   - :warning:注入

     ```javascript
     new Vue({
         el: '#app',
         store								//	ES5写法：store: store
     })
     ```

   - 组件的调用

     ```javascript
     methods: {
         increment() {
             this.$store.commit('increment')
             console.log(this.$store.state.count)
         }
     }
     ```

3. :whale:State的简单介绍

   - 从计算属性获取

     ```javascript
     const Counter = {
         template: `<div>{{ count }}</div>`,
         computed: {
             count () {							//	注意名称
     			return store.state.count		//	返回store.state中count变量的状态
             }
         }
     }
     ```

   - 通过【注入】的方式，访问store实例对象

     ```javascript
     Vue.use(Vuex)
     const app = new Vue({
         el: '#app',
         store,
         component: { Counter },
         template: `
     		<div class="app">
     			<counter></counter>
     		</div>
     	`
     })
     
     const Counter = {
         template: `<div>{{ count }}</div>`,
         computed: {
             count () {
                 return this.$store.state.count
             }
         }
     }
     ```

   - 【mapState】辅助函数

     ```javascript
     import { mapState } from 'vuex'
     
     export default {
         computed: mapState({
             count: state => state.count,		//	写法一
             countAlias: 'count',				//	写法二，等同于写法一
         })
         computed: mapState([
         	'count'							//	写法三，计算属性的名称和状态/state名称相同时，传递【字符串数组】
         ])
         computed: {
           	...mapState({					//	写法四，对象展开运算符
                 count: state => state.count
             }),
            	...mapState([
                 'count'
             ])
         }
     }
     ```

4. :whale:Getters简单介绍

   - 可以认为是【store的计算属性】，其返回值根据它的依赖被缓存起来，只有依赖改变，才会重新计算

   - 定义和访问

     ```javascript
     //	定义
     const store = new Vuex.Store({
         state: {
             todos: [
                 { id: 1, text: '...', done: true },
                 { id: 2, text: '...', done: false }
             ]
         },
         getters: {
             doneTodos: state => {
                 return state.todos.filter(todo => todo.done)
             }
         }
     })
     
     //	访问
     //	1、属性访问，作为Vue的部分缓存
     this.$store.getters.doneTodos
     //	2、方法访问（内部返回一个方法，外部通过方法访问），不作为Vue的部分缓存
     getters: {
         getTodoById: (state) => (id) => {
             return state.todos.find(todo => todo.id === id)
         }
     }
     store.getters.getTodoById(2)	//	结果【{ id: 2, text: '...', done: false }】
     ```

   - 【mapGetters()】辅助函数

     ```javascript
     import { mapGetters } from 'vuex'
     
     export default {
         computed: {
             ...mapGetters([					//	写法一，数组形式
                 'doneTodosCount',
                 'anotherGetter'
             ]),
             ...mapGetters({
                 doneCount: 'doneTodosCount'		//	写法二，对象形式
             })
         }
     }
     ```

     

5. :whale:Mutations简单介绍，同步事务

   - 简单调用

     ```javascript
     const store = new Vuex.Store({
         state: {
             count: 1
         },
         mutations: {
             increment (state) {
                 state.count++
             }
         }
     })
     
     //	不能直接调用mutations中的函数，要根据【type】调用【store.commit】方法，更改state
     store.commit('increment')
     ```

   - 提交载荷/传参/payload

     ```javascript
     mutations: {
         increment (state, n) {
             state.count += n
         }
     }
     
     //	调用，注意【参数个数】
     store.commit('increment', 10)
     
     //	另外一种调用/提交方式
     store.commit({
         type: 'increment',
         amount: 10
     })
     mutations: {
         increment (state, payload) {
             state.count += payload.amount
         }
     }
     ```

   - 常量替代Mutation事件类型，:book:参考

     > [Mutation | Vuex (vuejs.org)](https://vuex.vuejs.org/zh/guide/mutations.html#mutation-需遵守-vue-的响应规则)

   - 采用【mapMutations】辅助函数

     ```javascript
     import { mapMutations } from 'vuex'
     
     export default {
         methods: {
             //	写法一
             ...mapMutations([
                 'increment',				//	将【this.increment()】映射为【this.$store.commit('increment')】
                 'incrementBy'				//	将【this.incrementBy(amount)】映射为【this.$store.commit('incrementyBy', amount)】
             ]),
             ...mapMutations({
                 add: 'increment'			//	将【this.add()】映射为【this.$store.commit('increment')】
             })
         }
     }
     ```

6. :whale:Action简单介绍，异步事务

   - 和Mutation的区别

      - Action提交的是Mutation，不是【直接变更状态】
      - Action可以包含【异步操作】

   - 简单注册

      ```javascript
      const store = new Vuex.Store({
          state: {
              count: 0
          },
          mutations: {
              increment (state) {
                  state.count++
              }
          },
          actions: {
              incrementAsync (context) {
                  context.commit('increment')
              },
              add ({ commit }) {					//	ES2015的参数解构写法
                  commit('increment')
              }
          }
      })
      ```

   - 分发Action

     ```javascript
     store.dispatch('incrementAsync')					//	写法一
     store.dispatch('incrementAsync', {					//	写法一（载荷）
         amount: 10
     })
     store.dispatch({									//	写法二（载荷）
         type: 'incrementAsync',
         amount: 10
     })
     
     //	采用【mapActions】辅助函数
     export default {
         methods: {
             ...mapActions([
                 'incrementAsync',
                 'incrementAsyncBy'
             ]),
             ...mapActions([
                 add: 'incrementAsync'
             ])
         }
     }
     ```

   - 组合使用

     ```javascript
     //	假设【getData()】和【getOtherData()】返回的是【Promise】
     actions: {
         async actionA ({ commit }) {
             commit('gotData', await getData())
         },
     	async actionB ({ dispatch, commit }) {
             await dispatch('actionA')
             commit('gotOtherData', await getOtherData())
         }
     }
     ```

7. :whale:Module简单介绍

# 六、组件

1. 基本示例

   ```html
   <div id="app">
   	<button-counter></button-counter>
   </div>
   ```

   ```javascript
   Vue.component('button-counter', {						//	全局注册
   	data: function() {
   		return {
   			count: 0
   		}
   	},
       template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
   })
   ```

   - :warning:关于【组件的data】，是一个函数，用来维护每个组件实例的独立拷贝，:book:参考

     > [组件基础 — Vue.js (vuejs.org)](https://cn.vuejs.org/v2/guide/components.html#data-必须是一个函数)

   - :ice_cream:父子组件传值

     ```javascript
     //	子组件
     Vue.component('blog-post', {
         props: ['title'],								//	注意，是【props】
         template: '<h3>{{ title }}</h3>'
     })
     ```

     ```html
     <!-- 父组件 -->
     <blog-post title="My hourney with Vue"></blog-post>
     <blog-post title="Blogging with Vue"></blog-post>
     <blog-post title="Blogging with Vue"></blog-post>
     ```

   - :ice_cream:父子组件事件处理

     ```html
     <!-- 子组件 -->
     <button v-on:click="$emit('enlarge-text'， 0.1)">				//	触发【enlarge-text】事件，并提供数值
         Enlarge text
     </button>
     ```

     ```html
     <!-- 父组件，第一种写法 -->
     <blog-post v-on:enlarge-text="postFontSize += $event"></blog-post>			//	监听【enlarge-text】事件，$event捕获抛出的数值
     <!-- 第二种写法 -->
     <blog-post v-on:enlarge-text="onEnlargeText"></blog-post>
     ```

     ```javascript
     //	针对第二种写法的js部分
     methods: {
         onEnlargeText: function (enlargeAmount) {
             this.postFontSize += enlargeAmount
         }
     }
     ```

   - 组件使用【v-model】指令

     ```html
     <!-- 基础实现 -->
     <input v-model="searchText">
     <!-- 等价于 -->
     <input v-bind:value="searchText" v-on:input="searchText = $event.target.value">
     
     <!-- 自定义组件 -->
     <custom-input v-model="searchText"></custom-input>
     ```

     ```javascript
     //	自定义组件的定义
     Vue.component('custom-input', {
         props: ['value'],
         template: `<input v-bind:value="value" v-on:input="$emit('input', $event.target.value)"`
     })
     ```

   - 组件中的插槽

     ```html
     <alert-box>Something bad happened.</alert-box>
     ```

     ```javascript
     Vue.component('alert-box', {
         template: '<div class="demo-alert-box>"' +
         		'	<strong>Error!</strong>' +
         		'	<slot></slot>'	+
         		'</div>'
     })
     ```

   - 动态组件，:book:参考

     > [组件基础 — Vue.js (vuejs.org)](https://cn.vuejs.org/v2/guide/components.html#动态组件)

2. 深入了解

   - 组件名

     :ice_cream:kebab-case方式/短横线分割命名

     ```javascript
     Vue.component('my-component-name', { /* ... */ })
     ```

     :ice_cream:PascalCase方式/首字母大写命名

     ```javascript
     Vue.component('MyComponentName', { /* ... */ })
     ```

   - 【全局注册】与【局部注册】

     :ice_cream:全局注册：在任何新建的Vue实例中，都可以使用

     ```javascript
     Vue.component('my-component-name', { /* ... */ })
     ```

     :ice_cream:局部注册：全局注册的组件，用【webpack】构建系统时，即使不使用，也会存在于【构建结果中】，额外增加JS开销

     ```javascript
     var ComponentA = { /* ... */ }
     new Vue({
         ele: '#app',
         components: {
             'component-a': ComponentA				//	属性名为组件标签名，属性值为组件实例
         }
     })
     
     //	ES2015模块
     import ComponentA from './ComponentA.vue'
     export default({
         components: {
             ComponentA								//	简写
         }
     })
     ```

   - Prop

     :ice_cream:类型：1、为组件提供了文档；2、指定类型，遇到类型错误的时候，会在控制台提示用户

     ```javascript
     props: {
         title: String,
     	likes: Number,
     	isPublished: Boolean,
     	commentIds: Array,
     	author: Object,
     	callback: Function,
     	contactsPromise: Promise
     }
     ```

     :warning:父子组件间，数据【单向下行绑定】，父组件数据更新，子组件数据更新

     :ice_cream:验证：props接收对象

     ```javascript
     Vue.component('my-component', {
         props: {
             propA: [Number, String],						//	基础类型检查，【null】和【undefined】也能通过
             propB: {
                 type: String,
                 required: true,
                 default: 'demo'								//	必填，且有默认值
             },
             propC: {
                 type: Object,
                 default: function() {
                     return { message: 'hello' }
                 }
             },
             propD: {										//	自定义验证函数
                 validator: function(value) {
                     return ['success', 'warning', 'danger'].indexOf(value) !== -1
                 }
             }
         }
     })
     ```

   - 自定义事件：因为HTML对事件的大小写不敏感，且自动转换为小写，所以自定义事件推荐【kebab-case】的写法

     :ice_cream:原生事件绑定到组件：使用【.native】修饰符

     ```html
     <base-input v-on:focus.native="onFocus"></base-input>
     ```

     ```javascript
     //	如果监听失败，可能不会报错，相应函数也不会执行，通过【$listeners】property解决；它将所有【事件监听器】指向某个property，然后执行相应函数操作
     Vue.component('base-input', {
         inheritAttrs: false,				//	除了【label】和【value】之外的attributes，都以【键值对】方式存放在$attrs中
         props: ['label', 'value'],
         computed: {
             inputListeners: function() {
                 var vm = this
                 return Object.assign({}, 
     			this.$listeners,			//	父级添加的所有监听器
     			{
                     input: function(event) {		//	自定义监听器，或者覆写监听器
                         vm.$emit('input', event.target.value)
                     }
                 })
             }
         },
         template: '<label> ' +
         		'{{ label }} ' +
         		'<input v-bind="$attras" v-bind:value="value" v-on="inputListeners"> ' +
         		'</label>'
     })
     ```

     :ice_cream:.async修饰符：用来解决父子组件间变量的【双向绑定】问题

     ​	:warning:1、【.sync】不能和表达式一起使用；2、【.sync】不能用于【字面量】的对象上，例如：v-bind.sync="{ title: doc.title }"

     ```javascript
     //	方法一
     //	子组件
     this.$emit('update:title', newTitle)
     //	父组件
     ```

     ```html
     <text-document v-bind:title="doc.title" v-on:update:title="doc.title = $event"></text-document>
     
     //	方法二
     <text-document v-bind:title.sync="doc.title"></text-document>
     ```

     :book:参考

     > [自定义事件 — Vue.js (vuejs.org)](https://cn.vuejs.org/v2/guide/components-custom-events.html#sync-修饰符)

   - 插槽：略

   - 【动态组件】&【异步组件】

# 七、全局API

1. Vue.extend(options)

   - 参数：{ Object } options

   - 用法：使用基础Vue构造器，创建一个【子类/组件】；参数是包含【组件选项】的对象，如data、methods、template等等

   - 案例

     ```html
     <div id="mount-point"></div>
     ```

     ```javascript
     //	创建构造器
     var Profile = Vue.extend({
         template: '<p>{{firstName}} {{lastName}} aka {{alias}}</p>',
         data: function() {
             return {
                 firstName: 'Walter',
                 lastName: 'White',
                 alias: 'Heisenberg'
             }
         }
     })
     //	实例挂载
     new Profile.$mount('#mount-point')
     ```

     ```html
     <!-- 结果 -->
     <p>Walter White aka Heisenberg</p>
     ```

     

# 八、过滤器

1. 局部/本地过滤器

   ```vue
   //	使用方式两种，【插值表达式】和【v-bind指令】中
   <div v-bind:title="title | filter">{{ message | filter }}</div>
   //	定义
   filters: {
   	filter(value) {
   		if(!value) return ''
   		return value.charAt(0).toUpperCase() + value.slice(1)
   	}
   }
   ```

   - :ice_cream:可以多个过滤器串联

     ```vue
     <div>{{ message | filterA | filterB }}</div>
     ```

     

   - :ice_cream:过滤器可以带参数，filter函数定义中则有【两个】参数，一个是message，另一个是para

     ```vue
     <div>{{ message | filter(para) }}</div>
     ```

2. 全局过滤器

   ```
   Vue.filter('capitalize', function (value) {
   	if (!value) return ''
   	return value.charAt(0).upUpperCase() + value.slice(1)
   })
   ```

   

# 附录、其他

1. $nextTick()函数：

   - Vue更新DOM是异步操作，该函数在更新完毕后，进行回调。Vue在观察到数据变化时，不直接更新DOM，而是开启【异步更新队列】，缓冲同一事件中发生的所有数据改变

   - 使用方式

     ```vue
     <template>
     	<div>
             <div id="changeDom" v-if="showDiv">显示文本</div>
     		<button @click="showAndGetText">获取内容</button>
         </div>
         </div>
     </template>
     <script>
     export default {
         data () {
             return {
                 showDiv: false
             }
         },
         methods: {
             showAndGetText () {
                 this.showDiv = true
                 this.$nextTick(function () {						//	等待该【点击事件】完成所有数据更改并更新DOM后，回调该函数
                     let text = document.getElementById('changeDom').innerHTML
                     console.log('内容为：', text)
                 })
             }
         }
     }
     </script>
     ```

   - :book:参考
   
     > [(49条消息) $nextTick()的作用_splx2013的博客-CSDN博客_nexttick](https://blog.csdn.net/splx2013/article/details/107636868)
   
2. axios组件：

   - :book:参考

     > [POST 请求 | Axios 中文文档 | Axios 中文网 (axios-http.cn)](https://www.axios-http.cn/docs/post_example)
   
3. :warning:组件生命周期

   - created：实例【创建完】之后调用，【数据侦听、计算属性、方法、事件/侦听器的回调】已经完成；【挂载】还没开始且【$el.property】尚不可以用

   - mounted：实例【挂载】之后调用，【el】被创建的【vm.$el】替换；:warning:该周期不会保证所有子组件挂载完成，如果希望等到整个视图渲染完毕，可以使用【vm.$nextTick()函数】

   - beforeDestroy：实例销毁之前调用

   - 其他，:book:参考

     > [API — Vue.js (vuejs.org)](https://cn.vuejs.org/v2/api/#选项-生命周期钩子)

4. :warning:关于Uniapp的【uni.$emit】、【uni.$on】和【uni.$off】

   - uni.$on('event-name', functionName)，这里的只需要【functionName】，不需要加上括号

     ```javascript
     function fn() {					//	声明或定义
         //	code...
     }
     fn()							//	调用
     uni.$on('event-name', fn)		//	只需要函数名称，即函数声明或定义
     ```

   - uni.$off('event-name', functionName)

     :ice_cream:没有参数，移除所有的事件监听器，不限于某个组件

     :ice_cream:只提供了事件，移除该事件的所有监听器，不限于某个组件

     :ice_cream:同时提供了事件和回调函数，移除该回调的监听器，即移除该组件的该事件的监听器

     :ice_cream:提供的回调必须跟$on的回调必须为同一个才能移除这个回调的监听器

5. :book:官网API

   > [API — Vue.js (vuejs.org)](https://cn.vuejs.org/v2/api/#选项-DOM)

