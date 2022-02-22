# 零、表情符号介绍

- :book:参考
- :lollipop:一级分类
- :warning:注意

# 一、API介绍

- uni.getStorageSync(key)

  ```javascript
  uni.getStorageSync('userInfo')
  ```

  1. 从本地缓存中， 【同步】获取指定key的内容

- uni.setStorageSync(key, data)

  ```javascript
  uni.setStorageSynce('userInfo', userInfo)
  ```

  1. 将data覆盖存储在本地缓存中指定的key，同步接口
  2. **与【uni.setStorage(key, data)】区别：异步不会阻塞当前任务，性能更好；同步等到数据处理结束，才能继续其他任务，数据更安全**

- uni.clearStorageSync()

  ```javascript
  uni.clearStorageSync()
  ```

  1. 同步清理本地数据缓存

- this.setData(object, [callback])

  ```javascript
  Page({
  	data: {
  		text: 'init data'
  	},
  	changeText: function () {
  		// this.data.text = 'changed data'	//	不能直接修改【this.data.text】
  		this.setData({
  			text: 'changed data'
  		})
  	},
      addNewField: function () {
          this.setData({
              'newField.text': 'new data'
          })
      }
  })
  
  ```

  1. 【setData()函数】用于将数据，以【异步】方式，从逻辑层发送到视图层，同时改变对应的数据值
  2. 直接修改【this.data】而不调用【this.setData】是无法改变页面状态，造成数据不一致
  3. 仅支持设置可JSON化的数据
  4. 注意区分【this.setData(data)】和【this.setData({data})】，前者更新data键值对，后者更新data的键值

  - this.$debounce(callback, time, boolean)

# 二、简单的API

- uni.showToast()：显示消息提示框
- uni.showActionSheet()：底部向上弹出操作菜单
- uni.showModal()：显示模态弹窗，可以只有一个确定按钮，类似一个API整合了html中的alert和confirm
- uni.navigateTo()：保留当前页面，跳转到应用内的某个页面
- uni.navigateBack()：关闭当前页面，返回上一页面或多级页面
- uni.reLaunch()：关闭所有页面，打开到应用内的某个页面

# 三、其他

1. H5页面开发，:book:参考

   > [(50条消息) 使用uniapp开发微信公众号（H5页面），用微信开发者工具调试微信公众号_LzzMandy的博客-CSDN博客_uniapp 开发微信公众号](https://blog.csdn.net/LzzMandy/article/details/104989910)

