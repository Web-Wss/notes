# uni-app

## 简介

**uni-app 是一个使用 Vue.js进行 开发所有前端应用的框架**。开发者编写一套代码，即可发布到 iOS、Android、H5、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉/淘宝）、快应用等多个平台。


![image-20230210163433478](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101634632.png)

> 详细的 uni-app 官方文档，请翻阅 https://uniapp.dcloud.net.cn/



## 学习uniapp本质

1. 移动端技术太多，跨端框架或是未来发展趋势。
2. 一套代码多端发布受开发者青睐。
3. 完整的生态，受企业青睐

---

## uniapp优势

![image-20230210163555719](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101635823.png)

---

## uni-app和vue的关系

- 使用vueJS开发
- 在发布到H5时，支持所有vue语法
- 发布到App和小程序时，实现部分Vue语法

## uni-app和小程序有什么关系

- 组件标签靠近小程序规范
- 接口能力（JS API）靠近微信小程序开发
- 完整的小程序生命周期

## uniapp与web代码编写区别

![image-20230210163634428](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101636556.png)

## 课程内容

## 学习重点

1. 掌握uniapp技术本身，适配兼容安卓、IOS、html5、腾讯小程序4个平台
2. 掌握uniapp的前后台完整开发流程
3. 掌握组件化开发思路

## 知识点

1. 入门小程序

2. uniapp开发环境搭建

3. uni-app基础api学习

4. unicloud云开发平台学习

   1. unicloud基本使用方法
   2. 环境配置
   3. 高级方法使用

5. 平台适配

## 实战项目

### 项目演示

- h5访问地址：[[https://uni.duyiedu.com](https://uni.duyiedu.com)]([uni.duyiedu.com](uni.duyiedu.com))
- 安卓应用apk下载地址：[https://mp-4b2543b2-eec4-4dfa-bbc6-6e1d9847cc1d.cdn.bspapp.com/cloudstorage/__UNI__A49A088__20231122115317.apk](https://mp-4b2543b2-eec4-4dfa-bbc6-6e1d9847cc1d.cdn.bspapp.com/cloudstorage/__UNI__A49A088__20231122115317.apk)
- 微信小程序：小程序内搜索「渡一uniapp案例」

## 项目结构分析

### 首页面

- 搜索引导
  - 搜索界面
- 导航栏
  - 导航列表展示
  - 导航标签设置
- 文章列表
  - 文章收藏
  - 图文信息展示
- 文章详情
  - 作者关注
  - 富文本渲染
  - 文章评论
    - 评论回复
    - 指定评论回复
    - 评论发布
    - 评论组件展示

### 关注界面

- 文章
  - 文章列表展示
- 作者
  - 作者列表展示

### 我的界面

1. 登录
   - 个人信息展示
   - 我的文章
   - 意见反馈
     - 图片上传
     - 反馈信息上传
2. 未登录
   - 登录信息提示
   - 跳转登录界面

### 注册登录模块

1. 登录
   - 账号登录
     - 账号密码实现登录功能
   - 手机登录	
     - 手机号验证码实现登录功能

### 项目整体流程

1. 页面构建

2. 数据处理

3. 逻辑实现

4. 适配发行

   1. 多平台适配
   2. 多平台打包
   3. 多平台发布（安卓、IOS、小程序、h5)

   

## 课程讲解方式

- 项目为导向，只学习项目需要相关API
- 模块为核心，逐步实现项目
- css重复代码部分进行粘贴复制，其余全部实现手写

# 微信小程序简介

## 文档相关

1. 开发文档：https://developers.weixin.qq.com/miniprogram/dev/framework/
2. 微信公众平台：https://mp.weixin.qq.com/

## 开发者工具

​	下载地址：https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html

### 使用

**必选项处理**

![image-20230210164011622](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101640719.png)

**appID获取**

> 微信公众平台进行appID获取

![](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101641411.png)

### 小程序代码构成

> 参考地址：https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/code.html#JSON-%E9%85%8D%E7%BD%AE

1. `.json` 后缀的 `JSON` 配置文件
2. `.wxml` 后缀的 `WXML` 模板文件
3. `.wxss` 后缀的 `WXSS` 样式文件
4. `.js` 后缀的 `JS` 脚本逻辑文件



**小程序基本结构**

```html
<view class="container">
  <view class="userinfo">
    <button wx:if="{{!hasUserInfo && canIUse}}"> 获取头像昵称 </button>
    <block wx:else>
      <image src="{{userInfo.avatarUrl}}" background-size="cover"></image>
      <text class="userinfo-nickname">{{userInfo.nickName}}</text>
    </block>
  </view>
  <view class="usermotto">
    <text class="user-motto">{{motto}}</text>
  </view>
</view>
```



### 小程序基本操作

- **配置信息**

  - 全局配置 -> https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html

    ```json
    {
      "pages": [
        "pages/index/index",
        "pages/logs/index"
      ],
      "window": {
        "navigationBarTitleText": "Demo"
      },
      "tabBar": {
        "list": [{
          "pagePath": "pages/index/index",
          "text": "首页"
        }, {
          "pagePath": "pages/logs/index",
          "text": "日志"
        }]
      },
      "networkTimeout": {
        "request": 10000,
        "downloadFile": 10000
      },
      "debug": true
    }
    ```

    

  - 页面配置

    ```json
    {
      "navigationBarBackgroundColor": "#ffffff",
      "navigationBarTextStyle": "black",
      "navigationBarTitleText": "微信接口功能演示",
      "backgroundColor": "#eeeeee",
      "backgroundTextStyle": "light"
    }
    ```

- **全局生命周期函数**

  ```js
    /**
     * 当小程序初始化完成时，会触发 onLaunch（全局只触发一次）
     */
    onLaunch: function () {
      
    },
  
    /**
     * 当小程序启动，或从后台进入前台显示，会触发 onShow
     */
    onShow: function (options) {
      
    },
  
    /**
     * 当小程序从前台进入后台，会触发 onHide
     */
    onHide: function () {
      
    },
  
    /**
     * 当小程序发生脚本错误，或者 api 调用失败时，会触发 onError 并带上错误信息
     */
    onError: function (msg) {
      
    }
  ```

  - **页面生命周期函数** -> https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/page-life-cycle.html

  ```js
   onLoad: function(options) {
      // 页面创建时执行
    },
    onShow: function() {
      // 页面出现在前台时执行
    },
    onReady: function() {
      // 页面首次渲染完毕时执行
    },
    onHide: function() {
      // 页面从前台变为后台时执行
    },
    onUnload: function() {
      // 页面销毁时执行
    },
    onPullDownRefresh: function() {
      // 触发下拉刷新时执行
    },
    onReachBottom: function() {
      // 页面触底时执行
    },
    onShareAppMessage: function () {
      // 页面被用户分享时执行
    },
    onPageScroll: function() {
      // 页面滚动时执行
    },
    onResize: function() {
      // 页面尺寸变化时执行
    }
  ```

- **组件生命周期**->https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/lifetimes.html

  ```js
  Component({
    lifetimes:{
      created() {
        console.log('created,组件实例刚刚被创建好时， created 生命周期被触发')
      },
      attached() {
        console.log('组件实力进入页面节点树时候进行执行');
      },
      detached() {
        console.log('在组件实例被从页面节点树移除时执行');
      }
    }
  })
  ```

  

- **界面跳转**

  - 新界面打开=>https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html

    ```js
    调用 API wx.navigateTo
    使用组件 <navigator open-type="navigateTo"/>
    ```

  - 页面重定向

    ```js
    调用 API wx.redirectTo
    使用组件 <navigator open-type="redirectTo"/>
    ```

  - 页面返回

    ```
    调用 API wx.navigateBack
    使用组件<navigator open-type="navigateBack">
    用户按左上角返回按钮
    ```

  - Tab切换

    ```javascript
    调用 API wx.switchTab
    使用组件 <navigator open-type="switchTab"/>
    用户切换 Tab
    ```

  - 重启动

    ```js
    调用 API wx.reLaunch
    使用组件 <navigator open-type="reLaunch"/>
    ```

- **数据绑定**

  ```html
  <view>{{message}}</view>
  ```

  ```js
  Page({
    data:{
      message:"hello world"
    }
  })
  ```

- **条件渲染**

  ```html
  <view wx:if="{{isShow}}">条件判断显示</view>
  ```

  ```
  Page({
  	data:{
  		isShow:false
  	}
  })
  ```

  

- **列表渲染**

  ```html
  <view wx:for="{{list}}" wx:for-index="idx" wx:for-item="itemName">
    {{idx}}: {{itemName.name}}
  </view>
  ```

  ```js
  Page({
    data: {
      list:[
        {name:'a'},
        {name:'b'}
      ]
    }
  })
  ```


# uniapp开发规范

- 页面文件遵循Vue单文件组件（SFC）规范

- 组件标签靠近小程序规范 =>https://uniapp.dcloud.io/component/README

  ```vue
  <template>
  	<view>
  		页面内容
  	</view>
  </template>
  
  <script>
  	export default {
  		data() {
  			return {
  			}
  		},
  		methods: {	
  		}
  	}
  </script>
  
  <style>
  </style>
  ```

- 接口能力（JS API）靠近微信小程序规范 => https://uniapp.dcloud.io/api/README

  ```java
  uni.getStorageInfoSync()
  ```

- 数据绑定事件处理同Vue.js规范

  ```vue
  <template>
    <view @click="onClickFn">
        点击事件绑定
    </view>
  </template>
  
  <script>
  export default {
    methods: {
      onClickFn() {
        console.log('click事件')
      }
    }
  }
  </script>
  
  <style lang="scss" scoped>
  </style>
  ```

- 兼容多端运行，使用flex布局进行开发

## uniapp开发环境

### 开发工具

uni-app 官方推荐使用 **HBuilderX** 来开发 uni-app 类型的项目。主要好处：

- 模板丰富
- 完善的智能提示
- 一键运行

### 下载 HBuilderX

1. 访问 HBuilderX 的官网首页 https://www.dcloud.io/hbuilderx.html
2. 点击首页的 `DOWNLOAD` 按钮
3. 选择下载 `正式版`/alpha -> `App 开发版`
4. 将下载的 `zip包` 进行解压缩
5. 将解压之后的文件夹，存放到**纯英文**的目录中（且不能包含括号等特殊字符）
6. 双击 `HBuilderX.exe` 即可启动 HBuilderX
7. 详细安装文档：=> https://hx.dcloud.net.cn/Tutorial/install/windows

## 工程搭建

1. 文件 -> 新建 -> 项目

   ![image-20230210164710394](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101647480.png)

2. 填写项目基本信息

   ![image-20230210164806181](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101648279.png)

3. 项目创建成功

   ![image-20230210170218380](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101702469.png)



​	**基本目录结构**

```css
项目名称
----【pages】    内部存放所有页面
----【static】   存放所有静态资源，比如图片，字体图标
----【unpackage】存放所有打包生成后的文件
----app.vue     应用配置，用来配置App全局样式以及监听 应用生命周期
----main.js			Vue初始化入口文件
----mainfast.json  配置应用名称、appid、logo、版本等打包信息
----pages.json    配置页面路由、导航条、选项卡等页面类信息
----uni.scss      用途是为了方便整体控制应用的风格。比如按钮颜色、边框风格，uni.scss文件里预置了一批scss变量预置。
```



## 项目运行

### 浏览器运行

1. ![image-20230210165237132](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101652271.png)

### 小程序运行

1. 填写自己的微信小程序的 AppID：

   ![image-20230210165041953](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101650040.png)

2. 在 HBuilderX 中，配置“微信开发者工具”的**安装路径**：

   ![image-20230210165545670](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101655749.png)

3. 在微信开发者工具中，通过 `设置 -> 安全设置` 面板，开启“微信开发者工具”的**服务端口**：

   ![image-20230210165824853](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101658918.png)

4. 在 HBuilderX 中，点击菜单栏中的 `运行 -> 运行到小程序模拟器 -> 微信开发者工具`，将当前 uni-app 项目编译之后，自动运行到微信开发者工具中，从而方便查看项目效果与调试：

   ![image-20230210170117316](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101701394.png)

5. 初次运行成功之后的项目效果：

   ![image-20230210165342165](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302101653318.png)

### app真机运行

> ​	确保你的手机与电脑是在同一个局域网下面

1. 手机开启开发者模式
2. 选择数据管理
3. hbuildeX选择真机运行
4. 等待基座安装
5. 安装完成手机运行项目

### IOS模拟器运行

1.  Xcode下载
2.  定义版本进行模拟器运行

---

# 组件

文档参考地址：https://uniapp.dcloud.net.cn/component/

## 基础组件

> 基础组件在uni-app框架中已经内置，无需将内置组件的文件导入项目，也无需注册内置组件，随时可以直接使用，比如`<view>`组件。


**组件演示参考地址** => https://hellouniapp.dcloud.net.cn/pages/component/view/view

### 基础组件列表

- 视图容器
  - view 视图容器，类似于html中的div
  - scroll-view 可滚动试图容器 => https://uniapp.dcloud.net.cn/component/scroll-view
  - swiper 滑块视图容器，比如用于轮播banner
- 基础内容
  - icon 图标 => uni-icons
  - text 文字
  - rich-text 文字
  - progress 进度条
- 表单组件（Form）
  - button 按钮
  - checkbox 多项选择器
  - editor 富文本输入框
  - form 表单
  - input 输入框
  - label 标签
  - picker 弹出式聊表选择器
  - picker-view 窗体内嵌入式聊表选择器
  - radio 单项选择器
  - slider 滑动选择器
  - switch 开关选择器
  - textarea 多行文本输入框
- 路由与页面跳转（Navigation）
  - navigator 页面链接，类似于html中的a标签
- 媒体组件
  - audio 音频
  - camera 相机
  - image 图片
  - video 视频

### 组件公共属性集合

![image-20230213102859192](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131029353.png)

> 除了上述公共属性，还有一类特殊属性以`v-`开头，称之为vue指令，如v-if、v-else、v-for、v-model。

## 扩展组件

Demo地址：https://hellouniapp.dcloud.net.cn/pages/component/scroll-view/scroll-view

参考地址：https://ext.dcloud.net.cn/search?q=uni-icons

## 自定义组件

1. componets文件夹下定定义组件
2. 页面引用组件，无需倒入适量，直接使用即可
3. 其他操作（组件传值，事件绑定同vue）

## 基础API

**参考地址**：https://uniapp.dcloud.net.cn/api/README

### API列表

- **网络请求**

  - uni.request 发起网络请求

    > 为了解决uni.request网络请求API相对简单的问题，可使用@escook/request-miniprogram进行网路请求的处理
    >
    > 参考地址：https://www.npmjs.com/package/@escook/request-miniprogram
    >
    > **在小程序中，无法使用fetch及axios进行网络请求发送**

    **测试接口地址：https://study.duyiedu.com/api/herolist**

- 上传、下载

  - uni.unloadFile 上传文件  => https://uniapp.dcloud.net.cn/api/request/network-file
  - uni.downloadFile 下载文件

- 图片处理

  - uni.chooseImage 从相册选择图片，或者拍照 =>https://uniapp.dcloud.net.cn/api/media/image?id=chooseimage
  - uni.previewImage 预览图片
  - uni.getImageInfo 获取图片信息

- 数据缓存 => https://uniapp.dcloud.net.cn/api/storage/storage?id=setstorage

  - uni.getStorage 异步获取本地数据缓存
  - uni.getStorageSync 同步获取本地数据缓存
  - uni.setStorage 异步设置本地数据缓存
  - uni.setStorageSync 同步设置本地数据缓存
  - uni.removeStorage 异步删除本地数据缓存
  - uni.reoveStorageSync 同步删除本地数据缓存

- 交互反馈 => https://uniapp.dcloud.net.cn/api/ui/prompt?id=showtoast

  - uni.showToast 显示提示框
  - uni.showLoading 显示加载提示框
  - uni.hideToast 隐藏提示框
  - uni.hideLoading 隐藏加载提示框
  - uni.showModal 显示模态框
  - uni.showActionSheet 显示菜单列表

- 路由

  - uni.navigateTo 保留当前页面，跳转到应用内某个界面，使用uni.navigateBack 返回原页面

  - uni.redirectTo 关闭当前界面，跳转到应用内的某个界面

  - uni.reLaunch 关闭所有界面，打开应用内的某个界面

  - uni.switchTab 跳转到tab Bar页面

    

## 页面布局相关

**page**

> 页面容器css属性

```css
page:{
  height:100%;
  background-color:red;
}
```

**尺寸单位**

可使用单位：px rpx,upx, rem vh  vw

**外部样式文件引入**

同vue使用相同	

## uniapp生命周期

**参考地址：**https://uniapp.dcloud.net.cn/collocation/frame/lifecycle?id=%e5%ba%94%e7%94%a8%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f

### 应用生命周期

- onLaunch 初始化完成时触发（全局🈯️触发一次）

- onShow uni-app启动，或从后台进入前台显示

- onHide 当uni-app 应用从前台进入后台

  > 只能在App.vue里面进行监听，在其他界面监听无效

### 页面生命周期

- onLoad 监听页面加载（可获取上个界面传递的参数）
- onShow 监听页面显示，每次出现在屏幕上都进行触发
- onReady 监听页面初次渲染完成
- onHide 监听页面隐藏
- onUnload 监听页面卸载
- onReachBottom 页面滚动到底部事件

### 组件生命周期

- beofreCreate 
- created
- boforeMount
- mounted
- boforeDestroy
- destroyed


## uniApp特色

### 条件编译

> 条件编译是用特殊的注释作为标记，在编译时根据这些特殊的注释，将注释里面的代码编译到不同平台。

**语法**

<img src="https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131037225.png" alt="image-20230213103423907" style="zoom:50%;" />

**条件编译支持的文件**

- .vue
- .js
- .css
- pages.json
- 各预编译语言文件，如：.scss、.less、.stylus、.ts、.pug

> ​		条件编译是利用注释实现的，在不同语法里注释写法不一样，js使用 `// 注释`、css 使用 `/* 注释 */`、vue/nvue 模板里使用 `<!-- 注释 -->`；

#### 插件安装

1. ​	**scss安装**

   > 可以使用多种预编译处理器进行安装使用，以scss文件为例
   >
   > 下载地址：**https://ext.dcloud.net.cn/plugin?name=compile-node-sass**


## hbuilderX中使用unicloud云开发平台

### 文档

- 参考文档：https://uniapp.dcloud.io/uniCloud/README
- web控制台文档：https://dev.dcloud.net.cn/pages/common/login

### 传统业务开发流程

> ​	前端 => 后端 => 运维 => 发布上线

**使用unicloud云开发平台**

> 前端 => 运维 => 发布上线

### 什么是unicloud

> `uniCloud` 是 DCloud 联合阿里云、腾讯云，为开发者提供的基于 serverless 模式和 js 编程的实现后端服务的云开发平台。不需要服务器的购买配置即可快速创建一个完整的后端服务。

### unicloud优点

- 用JavaScript开发前后台整体业务
- 非h5项目免域名使用服务器
- 敏捷性业务处理，不需要前后端分离开发

## 开发流程

![image-20230213103914985](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131042219.png)



### uncloud构成

![image-20230213104002599](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131042188.png)

#### 云数据库

​	![image-20230213104045259](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131042233.png)



#### 云存储及CDN

> 可进行文件的相关存储操作

参考文档：https://uniapp.dcloud.io/uniCloud/storage

#### 创建云函数工程

1. **指定unicloud工程创建**

![image-20230213104404149](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131044255.png)

2. **保证uni-app应用标识appID填写**（保证用户为登录状态）

   ![image-20230213104515894](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131045944.png)

3. **进行云服务空间创建**

   ![image-20230213104434818](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131044921.png)

   > 如果未进行实名认证，会跳转至实名认证页面进行实名认证，等待实名认证审核之后可以开通服务空间。若腾讯云实名认证提示身份证下已创建过多账户，则需要在腾讯云官网注销不用的账户

4. 进行云函数创建

   ![image-20230213104602736](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131046847.png)

   ```js
   'use strict';
   // 一个通过nodeJS运行的函数在服务器端使用
   exports.main = async (event, context) => {
   	//event为客户端上传的参数
   	//context 包含了调用信息及运行状态,获取每次调用的上下文
   	console.log('event : ', event)
   	
   	//返回数据给客户端
   	return {
   		"code":0,
   		"msg":"云函数调用成功"
   	}
   };
   ```

   

5. **云WEB控制台查看**

   ![image-20230213104631613](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131046690.png)

6. **云数据库操作**

   > 在云数据库中进行数据操作，全部使用双引号进行值的定义

7. 云存储

   > 在云存储中进行文件的上传
   >
   > api使用：
   >
   > ```js
   > uniCloud.uploadFile({})
   > ```

8. 跨域处理

   参考文档https://uniapp.dcloud.io/uniCloud/quickstart?id=useinh5

## unicloud api操作

### 云函数调用

**参考文档**：https://uniapp.dcloud.net.cn/uniCloud/cf-functions?id=clientcallfunction

```js
// promise方式
uniCloud.callFunction({
    name: 'test', // 云函数名称
    data: { a: 1 }   // 请求参数
  })
  .then(res => {});

// callback方式
uniCloud.callFunction({
    name: 'test',
    data: { a: 1 },
    success(){},  // 成功
    fail(){},   // 失败
    complete(){}   // 完成（不管成功与失败）
});
```

### 云函数实现云数据库基本增删改查

#### 1. 获取数据库引用

```js
const db = uniCloud.database()
```

2. 获取数据库集合引用

   ```
   const collection = db.collection('unicloud-test-714') // uncloud-test-714 为数据表名称
   ```

3. 新增记录

   ```js
   const res = collection.add({user:'alan'})
   ```

   ```js
   'use strict';
   const db = uniCloud.database() // 获取数据库引用
   
   exports.main = async (event, context) => {
   	// 获取集合引用
   	const collection = db.collection('unicloud-test-714')
   	// 新增数据
   	const res = await collection.add({user:'alan'})
   	console.log(res)
   	return {
   		"code":0,
   		"msg":"云函数调用成功"
   	}
   };
   ```

4. 删除记录

   ```js
   	const res = await collection.doc('60ee51103b7d3500014124c1').remove()
   ```

5. 数据更新

   ```js
   const res = await collection.doc('60ee52a1827eca0001e56bc4').update({
   		name:"joob"
   	})
   
   const res = await collection.doc('60ee52a1827eca0001e56bc4').set({   // 如果说获取不到内容，从新进行插入记录的操作
   		name:"joob",
     	type:"javascript"
   	})
   ```

   > update与set的区别：
   >
   > 当没有找到指定记录时，使用update无法进行更新操作，set在没有查找到指定记录的时候，可以进行新增内容的操作（不存在进行创建添加操作）

6. 数据查找

   ```js
   // 查询全部
   	const res = await collection.get()
   // 指定条件进行查询-id查询
     const res = await collection.doc('id').get()  // id为需要查询的指定id
   // 指定条件查询-其他条件进行查询
     const res = await collection.where({name:"alan"}).get()
   ```

   #### 云存储操作

   1. 使用uni.chooseImage方法进行图片选择获取

      参考地址：https://uniapp.dcloud.io/api/media/image?id=chooseimage

      ```js
      	uni.chooseImage({
      					count: 1,
      					success(res) {
      						console.log(JSON.stringify(res.tempFilePaths))
      					}
      				})
      ```

   2. 使用uniCloud.uploadFile进行文件上传

      参考文档：https://uniapp.dcloud.io/uniCloud/storage?id=clouduploadfile

      ```js
      uni.chooseImage({
      					count: 1,
      					async success(res) {
      						let result = await uniCloud.uploadFile({
      							filePath:res.tempFilePaths[0],
      							cloudPath:'a.jpg',
      							success(res) {
      								console.log(res)
      							},
      							fail(err) {
      								console.log(err)
      							}
      						});
      					}
      				})
      ```

   3. 使用uniCloud.deleteFile进行图片删除

      参考文档：https://uniapp.dcloud.io/uniCloud/storage?id=clouddeletefile

      **阿里云函数删除不能在客户端进行删除操作，下列代码在云函数中进行使用**

      ```js
      let result = await uniCloud.deleteFile({
      	   fileList:['https://vkceyugu.cdn.bspapp.com/VKCEYUGU-6ce25980-c28e-4e78-bdef-a96eb40ad98b/06a1cb3a-84b7-47a0-b554-8aff299cb255.jpg'],
      	});
      	console.log(result)
      ```

## 项目启动-结构搭建

### 一、初始化数据库

1. 定义（选择）云服务空间

2. 初始化数据库

   1. 使用db_init.json文件 

      参考文档：https://uniapp.dcloud.io/uniCloud/hellodb?id=db-init

   2. 初始化db_init.json文件使用课程里面提供的文件即可

      source 文件夹 => db._init.json文件

      uniCloud目录找到database目录 添加db_init.json文件

      ![image-20230213104828561](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131048676.png)

### 二、静态文件配置

#### 1、static文件导入

> ​	导入项目中需要的图片文件
>
> ​	文件在当天课程资料source文件夹下进行查找
>
> ​	source文件目录：
>
> - app_logo =>**应用打包目录**
> - project_img => **工程所需图片文件**		

#### 2、css预编译处理器定义

1. uni.scss文件定义公共变量及混编方法

2. 每个页面下直接进行样式方法及变量使用

   ```scss
   /* 多行注释 */
   @mixin flex($level_style:space-between, $vertical_style:row, $isWrapper:nowrap) {
       display: flex;
       align-items: center;
       justify-content: $level_style;
       flex-wrap: $isWrapper;
       flex-direction: $vertical_style;
   }
   
   // $base-color:#ff6600;
   /* 全局系统样式定义 */
   $base-color:#f25037;
   ```

   

#### 3、page.json文件-tabBar创建

文档参考地址：https://uniapp.dcloud.net.cn/collocation/pages

> 在 `pages` 目录中，创建首页(home)、我的(self)、关注(follow)这 3 个 tabBar 页面。在 HBuilderX 中，可以通过如下的两个步骤，快速新建页面：



1. 在 `pages` 目录上鼠标右键，选择**新建页面**

2. 在弹出的窗口中，填写**页面的名称**、**勾选 scss 模板**之后，点击创建按钮。截图如下：

   ![image-20230213105800769](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131058829.png)

3. 配置tabBar效果，修改项目根目录中的 `pages.json` 配置文件，新增 `tabBar` 的配置节点如下：

   ```json
   "tabBar": {
       "color": "#666",
       "selectedColor": "#f25037",
       "backgroundColor": "#fff",
       "list": [   // 显示页面信息
         {
           "pagePath": "pages/tabBar/index/index",   // 页面路径
           "iconPath": "static/home.png",   // 默认图片
           "selectedIconPath": "static/home-active.png",  // 选中图片
           "text": "首页"   // 文字描述信息
         },
         {
           "pagePath": "pages/tabBar/follow/follow",
           "iconPath": "static/follow.png",
           "selectedIconPath": "static/follow-active.png",
           "text": "关注"
         },
         {
           "pagePath": "pages/tabBar/self/self",
           "iconPath": "static/my.png",
           "selectedIconPath": "static/my-active.png",
           "text": "我的"
         }
       ]
     }
   ```

4. 删除默认index界面

   1. 在 HBuilderX 中，把 `pages` 目录下的 `index首页文件夹` 删除掉
   2. 同时，把 `page.json` 中记录的 `index 首页` 路径删除掉

5. 修改globalStyle样式

   ```json
    "globalStyle": {
       "navigationBarTextStyle": "white",
       "navigationBarTitleText": "渡一教育",
       "navigationBarBackgroundColor": "#f25037",
       "backgroundColor": "#F8F8F8"
     },
   ```

#### 4、页面定义

> ​	创建tabBar需要的页面文件 
>
> index页面
>
> follow页面
>
> self页面

#### 5、index（首页）界面制作

- 导航栏-navBar组件实现

  > 同名组件名不需要使用import 进行导入

  ```css
  easyCom components/组件名/组件名.vue   // 特点：局部引入
  ```

  **微信及APP进行状态栏高度进行占位处理**

  方法参考地址：https://uniapp.dcloud.io/api/system/info?id=getsysteminfosync

  ```js
   // 获取手机系统信息
      const info = uni.getSystemInfoSync()
      // 设置状态栏高度
      this.statusBarHeight = info.statusBarHeight
  ```

  **胶囊信息获取**

  文档参考地址：https://uniapp.dcloud.io/api/ui/menuButton?id=getmenubuttonboundingclientrect

  **需要进行条件编译实现**

  ```js
  // (胶囊底部高度 - 状态栏的高度) + (胶囊顶部高度 - 状态栏内的高度) = 导航栏的高度
      this.navBarHeight = (menuButtonInfo.bottom - info.statusBarHeight) + (menuButtonInfo.top - info.statusBarHeight)
  ```

  **page.json进行前景色设置**

  ```json
  "navigationBarTextStyle": "white"
  ```

- **tabBar组件实现**

  > 配置tabBar效果，修改项目根目录中的 `pages.json` 配置文件，新增 `tabBar` 的配置节点如下：

```js
 "globalStyle": {
    "navigationBarTextStyle": "white",
    "navigationBarTitleText": "渡一教育",
    "navigationBarBackgroundColor": "#f25037",
    "backgroundColor": "#F8F8F8"
  },
"tabBar": {
    "color": "#666",
    "selectedColor": "#f25037",
    "backgroundColor": "#fff",
    "list": [   // 显示页面信息
      {
        "pagePath": "pages/index/index",   // 页面路径
        "iconPath": "static/home.png",   // 默认图片
        "selectedIconPath": "static/home-active.png",  // 选中图片
        "text": "首页"   // 文字描述信息
      },
      {
        "pagePath": "pages/follow/follow",
        "iconPath": "static/follow.png",
        "selectedIconPath": "static/follow-active.png",
        "text": "关注"
      },
      {
        "pagePath": "pages/self/self",
        "iconPath": "static/my.png",
        "selectedIconPath": "static/my-active.png",
        "text": "我的"
      }
    ]
  }
```

## 导航栏制作适配多端

### 一、导航栏组件创建

1. 定义导航栏组件

2. 引入导航栏组件

   ![image-20230213105942614](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131059734.png)


> 同名组件支持easycomment，不需要使用import方式进行导入即可使用

3. 结构搭建

   1. 图标使用

      uni-icons图标插件安装：[https://ext.dcloud.net.cn/plugin?id=28](https://ext.dcloud.net.cn/plugin?id=28)

4. 处理小程序显示错位问题

   **微信及APP应用实现状态栏高度占位处理**

   方法参考地址：[https://uniapp.dcloud.io/api/system/info?id=getsysteminfosync](https://uniapp.dcloud.io/api/system/info?id=getsysteminfosync)

   ![image-20230213110250401](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131102450.png)

   **微信小程序胶囊信息获取**

   文档参考地址:[https://uniapp.dcloud.io/api/ui/menuButton?id=getmenubuttonboundingclientrect](https://uniapp.dcloud.io/api/ui/menuButton?id=getmenubuttonboundingclientrect)

   ![image-20230213110201536](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131102606.png)

## 选项卡制作

![image-20230213111015648](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131110721.png)

### 一 、组件创建

> 1. 定义组件tabBar
> 2. index界面首页面进行组建引入

### 二、scroll-view组件使用

参考文档地址：https://uniapp.dcloud.io/component/scroll-view

> 使用scroll-view横向滚动的时候，需要注意，内部需添加一个容器对里面的滚动内容进行包裹

```vue
 <scroll-view class="tab-scroll" scroll-x="true">
      <view class="tab-scroll-box">
        <view v-for="(item, index) in navList" :key="index" class="tab-scroll-item">{{ item }}</view>
      </view>
 </scroll-view>
```

### 三、点击设置按钮跳转到标签设置界面

```vue
 <view class="tab-icons">
      <uni-icons @click="goLabelAdmin" type="gear" size="26" color="#666"></uni-icons>
    </view>

<script>
  // 创建labelAdmin界面之后进行跳转
  uni.navitageTo({url:'/pages/labelAdmin/labelAdmin'})
</script>
```

### 四、数据获取

1. 在page界面onLoad生命周期内进行_initLableList方法创建

2. 定义云函数，获取label表中的数据

   ```js
   'use strict';
   const db = uniCloud.database()
   exports.main = async (event, context) => {
   	const collection = db.collection('label')
   	const res = await collection.get()
   	
   	//返回数据给客户端
   	return {
   		code:0,
   		labelList:res.data
   	}
   };
   ```

3. page下的index界面进行数据获取，并将数据传递到tabBar组件，unicloud.callFunction方法进行数据获取

   ```json
   uniCloud.callFunction({
       name: "get_label_list",
       success:(res)=> {
      	 this.labelList = res.result.labelList
       }
   })
   ```

4. tabBar组件内部prop属性进行数据获取

   ```vue
   props: {
   			labelList: Array
   		}
   ```

## 请求方法封装

> 为了减少代码的冗余，优化代码的可读性，及可维护性，进行请求方法的封装

### 实现流程

#### 一、定义公共的http请求方法

1. 创建http.js文件，导出一个封装好的promise对象（内部进行uniCloud调用)

   ```js
   export default ({name,data={}})=> {
   	/* 导出pormise对象 */
   	return new Promise((resolve,reject) => {
   		uni.showLoading({
   		})
   		uniCloud.callFunction({
   			name,
   			success({result}) {
   				if(result.code === 0) {
   					resolve(result.data)
   				}else {
   					uni.showToast({icon:"none",title:result.msg})
   				}
   			},
   			fail(err) {
   				reject(err)
   			},
   			complete() {
   				uni.hideLoading()
   			}
   		})
   	})
   }
   ```

#### 二、创建接口文件进行公共方法的调用

![image-20230213114708707](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131147814.png)

#### 三、方法挂载到Vue原型上，供每个界面进行使用 

1. **使用webpacck的require.context方法对所有的请求函数收集**

   > require.context是什么？
   >
   > 一个webpack的api,通过执行require.context函数获取一个特定的上下文,主要用来实现自动化导入模块,在前端工程中,如果遇到从一个文件夹引入很多模块的情况,可以使用这个api,它会遍历文件夹中的指定文件,然后自动导入,使得不需要每次显式的调用import导入模块

   ```js
   /* 批量进行文件导出 */
   // . =>API目录的相对路径
   // true => 是否查询子目录
   // /.js/ => 需要查询的文件的后缀名
   
   const requireApi = require.context('.', true, /.js$/);
   console.log(requireApi.keys())
   let module = {};
   
   requireApi.keys().forEach((key, index) => {
   	if (key === './index.js') return
   	Object.assign(module, requireApi(key))
   })
   
   export default module
   ```

2. **main.js进行方法挂载**

   ```react
   import module from './ajax/api/index.js'
   Vue.prototype.$http = module;
   ```

   

#### 四、页面/组件内部进行方法的调用

```js
async _intiLabelList() {
				const labelList = await this.$http.get_label_list()
				this.labelList = labelList
			}
```



## 文章列表制作-容器组件

#### 一、定义articleList组件

1. **使用swiper组件实现滚动效果** https://uniapp.dcloud.io/component/swiper

   1. swiperItem数量动态话，当前的swiper数量应该与选项卡的数量相同

      获取选项卡的数量值，根据选项卡数量进行swiperItem渲染,index界面进行labelList传递

      ```react
      		<ArticleList :labelList="labelLIst" class="list-container"></ArticleList>
      ```

   2. ArticleList内根据swiper数量进行swiperItem渲染

      ```react
       <swiper class="swiper-container">
          <swiper-item v-for="(item,index) in labelList" :key="index">
            <view class="swiper-item uni-bg-red">
              <list-item></list-item>
            </view>
          </swiper-item>
        </swiper>
      ```

      

2. **选项卡与swiper组件联动效果实现**

   1. 选项卡点击事件绑定

      发送事件，调整activeIndex值，将activeIdnex值调整为父组件传递值

      swiper制定current属性，值为activeIndex

   2. swiper change事件监听，实现改变activeIndex属性

      ```react
       <swiper class="swiper-container" :current="activeIndex" @change="changCurrentIndex">
          <swiper-item v-for="(item,index) in labelList" :key="index">
            <view class="swiper-item uni-bg-red">
              <list-item></list-item>
            </view>
          </swiper-item>
        </swiper>
        
      <script>
        	 methods:{
            changeCurrentIndex(e) {
                const {current}  = e.detail;
                this.$emit('changeCurrentIndex',current)
           	 }
        		}
      </script>
      ```

      

#### 二、选项卡自动进行位置调整

1. scroll-view 组件添加属性 scroll-with-animation及 scroll-left 属性  https://uniapp.dcloud.io/component/scroll-view

2. 动态设置scrollintoview属性，为每一项添加ID属性进行跳转切换

   ```react
    <scroll-view class="tab-scroll" scroll-x="true" :scroll-into-view="currentIndex" :scroll-with-animation="true">
         <view class="tab-scroll-box">
           <view :id="`item${index}`" @click="navClickFn(index)" :class="{active:activeIndex === index}" v-for="(item, index) in labelList" :key="index" class="tab-scroll-item">{{ item.name}}</view>
         </view>
       </scroll-view>
   
   <script>
      watch:{
   	  activeIndex(index){
   		this.currentIndex = `item${index}`
   	  }
     },
     data() {
       return {
   		currentIndex:''
       }
     }
   </script>
   ```

3. 通过watch属性监听currIndex值改变，进行currentIndex设定

## 文章列表制作-文章卡片

#### 一、创建文章相关listItem组件

> ​	使用scroll-view 实现竖向滚动容器制作，注意在样式定义时进行多级高度设定

```vue
<view class="list-scroll-container">
		<scroll-view scroll-y="true" class="list-scroll">
			<view>
				<ListCard v-for="item in 50" :key="item"></ListCard>
			</view>
		</scroll-view>
</view>
```

#### 二、文章卡片组件定义

1. 创建基本样式及结构

2. 定义多状态卡片模块

   1. 通过父组件传递mode属性进行条件编译

   2. 根据条件进行选项卡卡片展示


#### 三、定义uniapp模版

1. 根目录下创建index.html文件
2. 参考地址：https://uniapp.dcloud.io/collocation/manifest?id=h5-template
3. manifest文件的html5配置中进行index.html文件引入

## 文章列表制作-数据渲染

#### 一、云函数创建

> ​	定义articleList云函数
>
> 删除不需要返回的文章详情内容

```react
'use strict';
const db = uniCloud.database()
exports.main = async (event, context) => {
	const list = await db.collection('article')
	.aggregate()
	.project({
		content:0
	})
	.end()
	//返回数据给客户端
	return {
		code:0,
		msg:"数据请求成功",
		data:list.data
	}
};

```

#### 二、前端进行数据获取

1. articleList组件 => created钩子中进行数据获取

   ```react
   created () {
       this._getArticleList()
     }
    methods: {
       async _getArticleList () {
         const articleList = await this.$http.get_article_list()
         this.articleList = articleList
       }
     }
   ```

#### 三、数据渲染

listItem组件中进行循环渲染使用

```react
<view class="list-scroll-container">
		<scroll-view scroll-y="true" class="list-scroll">
			<view>
				<ListCard :item="item" v-for="(item,index) in articleList" :key="index"></ListCard>
			</view>
		</scroll-view>
	</view>
```



#### 四、根据选项卡分类进行数据渲染

1. 添加全部分类选项

   ```react
   async _intiLabelList() {
   				const labelList = await this.$http.get_label_list()
   				this.labelList = [{name:"全部"},...labelList]
   			}
   ```

2. 请求articleList时进行数据传递 

   1. 为了保证导航数据的正确获取，调整created函数的_getArticle_list方法在watch中进行调用

      ```react
       watch: {
          labelList(newVal,OldVal) {
          this._getArticleList()
          },
        },
      ```

      

3. 云函数进行数据过滤调整

   ```js
   'use strict';
   const db = uniCloud.database()
   exports.main = async (event, context) => {
   	
   	const {classify} = event
   	
   	let matchObj = {}
   	
   	if(classify !== '全部') {
   		matchObj = {classify}
   	}
   	
   	const list = await db.collection('article')
   	.aggregate()   // 使用聚合的形式进行数据的获取
   	.match(matchObj)   // 根据匹配条件进行数据返回
   	.project({
   		content:0    // 本次查询不需要返回文章详情给前端
   	})
   	.end()
   	//返回数据给客户端
   	return {
   		code:0,
   		msg:"数据请求成功",
   		data:list.data
   	}
   };
   
   ```

4. 前端对数据进行缓存处理

   将原有接受内容数组转换为对象进行存储。每次change改变内容时进行判断操作处理

   使用$set方法进行对象的页面重新渲染

   ```js
   async _getArticleList (currentIndex) {
         const articleList = await this.$http.get_article_list({classify:this.labelList[currentIndex].name})
         this.$set(this.articleData,currentIndex,articleList)
       }
   ```




## 文章列表制作-上拉加载更多



#### 一、使用uni-load-more插件

下载地址：https://ext.dcloud.net.cn/plugin?id=29

使用：

```react
<uni-load-more status="loading"></uni-load-more>
```

#### 二、修改参数传递

1. 前端添加page及size属性到云函数

2. 云函数内进行返回值限制处理

   ```js
   const list = await db.collection('article')
   		.aggregate() // 使用聚合的形式进行数据的获取
   		.match(matchObj) // 根据匹配条件进行数据返回
   		.project({
   			content: 0 // 本次查询不需要返回文章详情给前端
   		})
   		.skip(pageSize * (page - 1)) // 首页从0开始计算
   		.limit(pageSize) // 每页最多返回多少条数据
   		.end()
   ```

3. 监听scroll-view的scrolltolower事件，触底时进行新的数据请求，当前的page值

4. 前端调整数据处理将直接赋值变为追加数据

   ```js
    // 填充数据时改变为追加数据
         let oldList = this.articleData[currentIndex] || []
         oldList.push(...articleList)
         this.$set(this.articleData, currentIndex, oldList)
   ```


#### 三、分类页数处理

1. 创建每一个分类的存储对象，含page及加载状态

   ```js
   loadData:{
   	page:1,
   	loading:loading
   }
   ```

2. 处理数据全部加载完成状态

   ```react
   // 判断当前后端没有返回数据处理 
         if(!articleList.length) {
           this.loadData[currentIndex] = {
             loading:"noMore",
             page:this.loadData[currentIndex].page
           }
           this.$forceUpdate()
           return 
         }
   ```


## 用户登录-登录界面搭建

#### 一、结构样式代码编写

1. uni-forms插件下载

   **下载地址**：https://ext.dcloud.net.cn/plugin?id=2773

2. send-code组件封装

   1. 结构处理

      ```js
      <template>
        <view class="code-container">
          <view class="vCode-btn" @click="getForm">
            {{runTime? `${time}秒后重新获取`:'获取验证码'}}
          </view>
        </view>
      </template>
      ```

   2. 定时器创建

   3. 组件销毁时，进行副作用（定时器）清除操作

      ```js
      // 离开界面时进行定时器的清除操作
        beforeDestroy () {
          clearInterval(this.timeId)
          this.timeId = null
          this.runTime = false
          this.time = 60
        },
      ```




   ## 用户登录-表单验证

   

   #### 一、userRulesMixin文件使用

   1. common文件夹下创建userRulesMixin

   ```react
   export default {
     install (Vue) {   // 使用install的形式进行安装mixin
       Vue.mixin({
         data () {
           return {
             a:'hello world'
           }
         },
         methods: {
           test () {
   
           }
         }
       })
     }
   }
   ```

   2. main.js中使用mixin文件

      ```react
      import userMixin from './common/rulesMixin.js'
      Vue.use(userMixin)
      ```

   3. 组件或页面内直接进行使用

      ```react
        onLoad: function () {
          console.log(this.test())
        }
      ```

   #### 二、验证规则编写

   ```react
     userRules: {
               loginName: {
                 rules: [
                   { required: true, 'errorMessage': "账户名不能为空" },
                   {
                     validateFunction: (rule, val, data, callback) => {
                       switch (true) {
                         case val.length < 6:
                           callback('用户名长度不正确')
                           break;
                         default:
                           return true
                       }
                     }
                   }   // 自定义验证规则
                 ]
               }
             }
   ```

   

   **手机号码正则表达式**

   ```css
   /^(0|86|17951)?(13[0-9]|15[012356789]|166|17[3678]|18[0-9]|14[57])[0-9]{8}$/
   ```

   

   ## 用户登录-账户名密码登录

   

   #### 一、前端数据整理

   1. 定义发送函数，将用户信息以及本次请求的用户登录类型传递给后端

      ```react
        this._sendUserInfo({ ...res, type: this.type })
      ```

   2. 创建请求方法 user_login

   3. 定义user_login函数

      ```react
      'use strict';
      // 获取数据库引用
      const db = uniCloud.database()
      exports.main = async (event, context) => {
        const { loginName, password, phone, type } = event;
      	
        const { affectedDocs, data } = await db.collection('user')
          .aggregate()
          .match(type === 'account' ? { loginName, password } : { phone })
          .end()
      	
        //返回数据给客户端
        return affectedDocs ? {
          code: 0,
          msg: "获取用户信息成功",
          data: data[0]
        } : {
          code: 1,
          msg: type === 'account' ? '获取用户信息失败，请检查用户名或密码' : '验证码或手机号码错误'
        }
      };
      
      ```

   4. 前端接收返回信息，进行数据处理

      1. 跳转界面到上一个历史记录
      2. 存储用户信息

   #### 二、使用store进行用户信息存储

   1. 创建实例化Store对象	

      ```react
      import Vue from 'vue'
      import VueX from 'vuex'
      import state from './state.js'
      import mutations from './mutations.js'
      import actions from './actions.js'
      
      
      Vue.use(VueX)
      
      export default new VueX.Store({
        state,
        actions,
        mutations
      })
      ```

   2. main.js中进行store注册

   3. 获取用户信息之后，进行用户信息保存操作

      ```js
      // login.vue
      
         async _sendUserInfo (data) {
            const res = await this.$http.user_login(data)
            if (res) {
              this.updateUserInfo(res)
              uni.showToast({
                title: '登录成功', icon: 'none',
              })
              setTimeout(() => { 
                 // #ifdef H5
                uni.switchTab({
                  url: '/pages/index/index'
                })
                // #endif
                // #ifndef H5
                uni.navigateBack()
                // #endif
              }, 2000)
            }
          }
          
      // mutation.js
      
      export default {
        updateUserInfo(state,userInfo) {
          uni.setStorageSync('userInfo',userInfo);
          state.userInfo = userInfo;
        }
      }
      ```

      ​	

   ## 用户登录-手机验证码登录

   

   #### 一、验证码处理

   1. 获取手机验证状态

   2. 保证send-code获取form对象

      ```react
      // SendCode.vue  
      this.$emit('getForm', form => this._sendCode(form))
      ```

   3. 通过form进行手机号码单独验证，并获取手机号码

      ```js
      const { phone } = await form.validateField(['phone']);
      ```

   4. 启动定时器，调整文本显示内容

      ```js
       const timeId = setInterval(() => {
              if (this.time === 1) {
                clearInterval(timeId)
                this.runTime = false
                this.time = 60
                return
              }
              this.time--
            }, 1000)
      ```

   #### 二、数据发送

   1. 数据发送，创建云函数

   2. 定义unicloud短信服务

      1. unicloud开发中心地址：https://dev.dcloud.net.cn/uniSms
      2. 短信参考配置地址：https://uniapp.dcloud.net.cn/uniCloud/send-sms

   3. 前端接受返回值，保存验证码，加入验证码验证规则

   4. 提交用户数据发送，指定参数phone及 type类型




   ## 收藏按钮组件实现

   ### 一、前端处理

   1. 收藏图标点击事件内获取用户信息，及文章信息，传递到后端

      由于多个界面中都会用到userInfo对象，可将userInfo对象放在一个全局的mixin中进行封存，保证每个界面或组件内部都可以进行使用

      1. 定义commonMixin文件

         ```js
         import { mapState } from 'vuex'
         
         export default {
           install (Vue) {
             Vue.mixin({
               computed: {
                 ...mapState(['userInfo'])
               }
             })
           }
         }
         ```

      2. main.js文件中对common Mixing文件进行使用

         ```js
         // main.js
         import commonMixin from './common/commonMixin.js'
         Vue.use(commonMixin)
         ```

         

   2. 将用户ID及文件ID作为参数传递给云函数

      1. 创建全局检测用户是否登录函数，供多个组件进行使用，commonMixin中完成

         ```js
         // commonMixin文件
         checkedIsLogin () {
                   return new Promise(resolve => {
                     if (this.userInfo) {
                       resolve()
                     } else {
                       uni.navigateTo({
                         url: '/pages/userInfo/login/login'
                       })
                     }
                   })
                 }
         // saveLike组件
         await this.checkedIsLogin();
         ```

      2. 将文章信息传递到saveLike组件内部使用

         ```js
         //listCard 组件
         <SaveLikes :item="item"></SaveLikes>
         // saveLike组件
          props: {
             item: Object
           }
         ```

      3. 发送数据到云服务器

         ```js
          const res = await this.$http.upate_save_like({
                 articleId: this.item._id,
                 userId: this.userInfo._id
               })
         ```

      

   ### 二、云函数定义

   1. 获取用户记录值

   2. 找到指定字段article_likes_ids

   3. 通过db.command 更新指令修改article_likes_ids

      参考地址：https://uniapp.dcloud.io/uniCloud/cf-database?id=query-command

      - 当文章id存在，进行删除操作，使用pull方法 参考地址：https://uniapp.dcloud.io/uniCloud/cf-database?id=pull
      - 当文章id不存在，进行添加操作，使用addToSet方法 参考地址:https://uniapp.dcloud.io/uniCloud/cf-database?id=addtoset

   4. 处理完成，将article_likes_ids进行修改之后，重新存储

      ```js
      'use strict';
      // 定义数据库引用
      const db = uniCloud.database();
      // 定义修改指令
      const dbCmd = db.command
      
      exports.main = async (event, context) => {
      	const {
      		userId,
      		articleId
      	} = event
      	// 获取用户Ids集合
      	const userInfo = await db.collection('user').doc(userId).get();
      
      	const articleIds = userInfo.data[0].article_likes_ids
      	let returnMsg = null
      
      	let articleArr = null;
      	// 如果包含删除收藏
      	if (articleIds.includes(articleId)) {
      		articleArr = dbCmd.pull(articleId)
      		returnMsg = '取消收藏成功'
      	} else {
      		articleArr = dbCmd.addToSet(articleId)
      		returnMsg = '添加收藏成功'
      	}
      
      	await db.collection('user').doc(userId).update({
      		article_likes_ids: articleArr
      	})
      
      	const updateUserInfo = await db.collection('user').doc(userId).get()
      
      	//返回数据给客户端
      	return {
      		code: 0,
      		data: {
      			msg: returnMsg,
      			newUserInfo:updateUserInfo.data[0]
      		}
      	}
      };
      
      ```

   ### 获取数据后前端处理

   1. 修改存储的用户信息article_likes_ids数组

      ```js
      // saveLikes组件处理
      this.updateUserInfo({ ...this.userInfo, ...newUserInfo })
      ```

   2. 弹出提示信息

   3. 重新对保存状态icon图标赋值

      使用计算属性处理用户收藏保存状态

      ```js
       computed: {
          isLike () {
            return this.userInfo && this.userInfo.article_likes_ids.includes(this.item._id)
          }
        }
      ```


   ## 搜索页面-结构搭建

   ### 一、调整navBar为动态组件

   > 添加是否为搜索界面判断

   1. isSearch，当界面为搜索界面时，添加返回icon图标

   ```html
    <!--当界面为搜索界面的时候，添加回退按钮  -->
         <view :style="{top:statusHeight + 'rpx'}" class="return-icon" v-if="isSearch">
           <uni-icons type="back" size="22" color="white"></uni-icons>
         </view>
   
   <style>
      /* 搜索界面单独添加样式 */
       .return-icon {
           position: absolute;
           left: 0;
           top: 50%;
           height: 60rpx;
           @include flex(center);
       }
   </style>
   ```

      2. 为点击事件添加条件处理，当为搜索界面时，阻止跳转事件
    
         ```js
         	if (this.isSearch) return
         				uni.navigateTo({
         					url: '/pages/search/search'
         				})
         ```

   3. 调整样式处理，根据条件添加🔙按钮，并绑定返回事件

      ```html
         *<!--当界面为搜索界面的时候，添加回退按钮  -->*
      
         ​      *<*view @click="returnArticleList" :style="{top:statusHeight + 'rpx'}" class="return-icon" v-if="isSearch"*>*
      
         ​        *<*uni-icons type="back" size="22" color="white"*></*uni-icons*>*
      
         ​      *</*view*>*
      
      
      ```

   4. 添加回退事件，根据平台使用指定事件

      ```js
      	// 返回文章列表界面
      			returnArticleList() {
      				// #ifdef H5
      				uni.switchTab({
      					url: '../../pages/index/index'
      				})
      				// #endif
      				// #ifndef H5
      				uni.navigateBack()
      				// #endif
      
      			}
      ```

      

   ### 二、搜索界面结构搭建

   > ​	根据当前状态，进行内容条件渲染

   ```html
     <view class="search-container">
       <!-- 搜索导航组件 -->
       <NavBar :isSearch="isSearch"></NavBar>
       <!-- 搜索包裹 -->
       <view class="search-wrapper">
         <!-- 没有进行搜索的操作 -->
         <view v-if="false" class="search-history-container">
           <!-- 头部 -->
           <view class="search-header">
             <text class="history-text">搜索历史</text>
             <text class="history-clean">清空</text>
           </view>
           <!-- 内容部分 -->
           <view class="search-history-content">
             <view class="history-content-item" v-for="item in 10" :key="item">直播</view>
           </view>
   
           <view class="no-data">当前没有搜索历史</view>
         </view>
   
         <!-- 开始进行搜索的操作 -->
         <view v-else class="search-list-container">
           <ListItem v-if="searchList.length"></ListItem>
            <view v-else class="no-data">没有搜索到相关数据</view>
         </view>
       </view>
     </view>	
   ```

   ## 搜索界面-业务逻辑处理

   ### 一、获取文本输入内容

   ​	input组件参考地址：[https://uniapp.dcloud.io/component/input?id=input](https://uniapp.dcloud.io/component/input?id=input)

   1. 添加右下角点击按钮事件

   2. 调整右下角显示文字

   3. 父子组件实现数据双向绑定

      ```js
      // NavVar组件
       computed: {
          // 动态获取searchvalue内容
          searchVal: {
            get () {
              return this.parentVal
            },
            set (val) {
              this.$emit('updateVal', val)
              if (!val) {
                this.$emit('sendSearchData')
              }
            }
          }
        }
      ```

   4. 处理空数据内容，清空操作后返回一个空的searchList

   ### 二、云函数定义并返回数据

   1. 定义云函数

   ```js
    const list = await db.collection('article')
       .aggregate() // 使用聚合的形式进行数据的获取
       // 使用正则表达式进行模糊匹配，只要是包含，就进行返回操作
       .match({ title: new RegExp(searchVal) })
       .project({
         content: 0 // 本次查询不需要返回文章详情给前端
       })
       .end()
   ```

   2. 前端进行数据渲染处理

      ```js
        async _sendSearchData (val) {
            if (!this.parentVal) {
              this.searchList = []
              return
            }
             const { articleList, total } = await this.$http.get_search_data({ searchVal: this.parentVal })
            this.searchList = articleList
            this.total = total
          }
      ```

   ### 三、处理历史记录切换显示

   1. 定义现实状态标识

      ```js
      // searchPage
       data() {
         return {
           isShowHistory:true,
            historyList:[],
         }
       }
      ```

   2. 点击卡片生成历史记录

      通过自定义事件形式传递数据到search界面

      ```js
       openHistory(val) {
            this.parentVal = val
            this._sendSearchData()
          }
      ```

   3. 点击卡片实现搜索内容保存

      ```js
      // searchPaage  
      openHistory(val) {
            this.parentVal = val
            this._sendSearchData()
          }
      // mutaitions.js处理
        // 设置历史收藏信息
        setHistory (state, val) {
          let list = state.historyList;
          // 判断是否包含当前搜索的内容，包含直接不执行任何操作
          if (list.length > 0 && list.findIndex(item => item === val) > -1) return
          list.unshift(val);
          uni.setStorageSync('historyList', list)
          state.historyList = list;
        },
       // state.js进行初始值绑定
       export default {
        historyList: uni.getStorageSync('historyList') || []
      }
      ```

   4. 点击历史记录文字实现搜索功能

      ```js
        // 弹出搜索内容
          openHistory(val) {
            this.parentVal = val
            this._sendSearchData()
          },  
      ```

      

   5. 实现点击清空按钮处理清空历史记录操作，通过listCard发送自定义事件，searchPage接收到自定义事件后，通过出发mutation里面的指定事件，进行state的指定属性清空操作

      ```js
      // mutations.js
        // 清空搜索历史信息
        cleanHistory (state) {
          uni.removeStorageSync('historyList')
          state.historyList = []
          uni.showToast({
            title: "清空完成",
            icon: "success"
          })
        }
      ```

      ## 标签页面-结构搭建

      ### 一、创建标签页面，完成结构样式处理

      1. 判断用户是否登录，未登录直接跳转登录界面

      2. 显示结构及样式处理

      3. 隐式样式处理


      ### 二、控制标按钮状态
    
      1. 添加状态属性监听，实现切换按钮文本及是否进行标签提修改发送操作
    
      ### 三、调整labelList为全局公共状态
    
      1. store定义labelList属性
      2. 在articleList界面进行labelList引用替换

   ## 标签页面-选项卡业务逻辑处理

   ### 一、创建我的标签及推荐标签数组

   1. 使用计算属性进行数组创建

      ```js
      selfLabelList () {
            return this.labelList.filter(item => this.labelIds.includes(item._id))
          },
          recommentLabelList () {
            return this.labelList.filter(item => !this.labelIds.includes(item._id) && item._id)
          },
      ```

   2. 初始化定义本地数据对象

      > 为了不影响用户数据，页面内定义属性进行用户数组信息数据拷贝,watch中进行调用,为了防止用户在修改之后，进行用户的改变无法获取准确的内容，通过watch中进行拷贝操作，并使用immediate初始话进行watch使用

      ```js
        watch: {
          userInfo: {
            immediate: true,
            handler (newVal, oldVal) {
              this.labelIds = [...(this.userInfo.label_ids)]
            }
          }
        },
      ```

   3. 进行页面数据渲染

      ```html
      // 用户标签组
              <view class="label-content-item" v-for="(item,index) in selfLabelList" :key="index">
                {{item.name}}
                <uni-icons @click="deleteLabelItem(item)" v-if="isEdit" class="icon-close" type="clear" size="20" color="red"></uni-icons>
              </view>
              <view v-if="!selfLabelList.length" class="no-data">当前没有数据</view>
            </view>
      
      // 推荐标签组
      <view class="label-content">
              <view class="label-content-item" @click="changeSelfList(item)" v-for="(item,index) in recommentLabelList" :key="index">
                {{item.name}}
              </view>
              <view v-if="!recommentLabelList.length" class="no-data">当前没有数据</view>
      </view>
      ```

   4. 为标签切换添加点击事件

      > 标签切换过程中需要注意，在isEdit情况下在进行标签切换操作。，追加用户标签，直接修改labelIds,删除标签，直过滤匹配内容。在未点击保存按钮的时候，不需要进行振正数据存储

      ```js
       //修改当前用户的labelList 
          changeSelfList (item) {
            if (!this.isEdit) return
            this.labelIds.push(item._id)
          },
          // 删除用户选项内容
          deleteLabelItem (item) {
            this.labelIds = this.labelIds.filter(val => val !== item._id)
          }
      ```

   ### 二、数据发送

   1. 前端收集数据，当前用户ID，及现阶段收藏的数组 selfIds

      ```js
       const label_ids = this.selfLabelList.map(item => item._id)
            const res = await this.$http.update_label_ids({ userId: this.userInfo._id, label_ids });
           
      ```

   2. 创建云函数。修改数据库中用户label_ids字段

      ```js
      'use strict';
      const db = uniCloud.database()
      exports.main = async (event, context) => {
      	//event为客户端上传的参数
      	const {userId,label_ids} = event
      	
      	const res = await  db.collection('user').doc(userId).update({
      		label_ids
      	})
      	//返回数据给客户端
      	return {
      		code:0,
      		data:{
      			msg:"修改成功"
      		}
      	}
      };
      ```

   3. 前端接收返回值，重新调整userInfo即可。

      ```js
       uni.showToast({
              title: res.msg
            })
            this.updateUserInfo({ ...this.userInfo, label_ids });
      ```

   ### 三、处理其他界面副作用

   1. ​	调整index界面labelList获取方式,判断是否包含用户信息，不包含直接返回，否则，显示用户搜藏内容

      ```js
      computed: {
          labelList () {
            if (this.userInfo) {
              this.activeIndex = 0;
              return [...this.$store.state.labelList.slice(0,1),...this.$store.state.labelList.filter(item => this.userInfo.label_ids.includes(item._id))]
            } else {
              return this.$store.state.labelList
            }
          },
      ```

   2. article页面内部兼听到userList改变值后，清空列表对象

      ```js
        watch: {
          labelList (newVal, OldVal) {
            this.articleData = {}
            this.loadData = {}
            this._getArticleList(this.activeIndex)
          },
        },
      ```


   ## 文章详情页面-结构样式处理

   

   **demo**

   ![image-20230213115321365](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131153486.png)

   ### 一、基本结构

   ​		

   ```html
   <template>
   	<view class="article-detail-container">
   		<view class="detail-title">
   			ssr基本介绍以及API的使用
   		</view>
   		<view class="detail-header">
   			<view class="detail-logo">
   				<image src="../../static/img/logo.jpeg" mode="aspectFill"></image>
   			</view>
   			<view class="detail-header-content">
   				<view class="detail-header-content-title">
   					WEB讲师
   				</view>
   				<view class="detail-header-content-info">
   					<text>2020.03.16 17:50</text>
   					<text>173 浏览</text>
   					<text>6 赞</text>
   				</view>
   			</view>
   			<button type="default" class="detail-header-button">取消关注</button>
   		</view>
   		<view class="detail-content-container">
   			<view class="detail-html">
   				文本内容
   			</view>
   		</view>
   
   		<!-- 评论组件 -->
   		<view class="detail-bottom">
   			<view class="input-container">
   				<text>谈谈你的看法</text>
   				<uni-icons type="compose" size="16" color="#f07373"></uni-icons>
   			</view>
   			<view class="detail-bottom-icons">
   				<view class="detail-bottom-icon-box">
   					<uni-icons type="chat" size="22" color="#f07373"></uni-icons>
   				</view>
   				<view class="detail-bottom-icon-box">
   					<uni-icons type="heart" size="22" color="#f07373"></uni-icons>
   				</view>
   				<view class="detail-bottom-icon-box">
   					<uni-icons type="hand-thumbsup" size="22" color="#f07373"></uni-icons>
   				</view>
   			</view>
   		</view>
   	</view>
   </template>
   ```

   

   ### 二、初始化样式

   ​	

   ```css
   .article-detail-container {
   	padding: 30rpx 0 108rpx;
   }
   
   .detail-title {
   	padding: 0 30rpx;
   	font-size: 36rpx;
   	font-weight: bold;
   }
   
   .detail-header {
   	@include flex(flex-start);
   	margin-top:20rpx;
   	padding: 0 30rpx;
   	.detail-logo {
   		flex-shrink: 0;
   		width: 80rpx;
   		height: 80rpx;
   		border-radius: 50%;
   		overflow: hidden;
   		image {
   			width: 100%;
   			height: 100%;
   		}
   	}
   	.detail-header-content {
   		width: 100%;
   		padding-left: 20rpx;
   		@include flex(space-between,column);
   		font-size: 24rpx;
   		align-items: flex-start;
   		.detail-header-content-title {
   			font-size: 28rpx;
   			color: #333;
   		}
   		.detail-header-content-info {
   			color: $c-9;
   			text {
   				margin-right: 20rpx;
   			}
   		}
   	}
   	.detail-header-button {
   		padding: 0 30rpx;
   		flex-shrink: 0;
   		height: 60rpx;
   		line-height: 60rpx;
   		border-radius: 10rpx;
   		font-size: 24rpx;
   		color: #FFFFFF;
   		background-color: $base-color;
   	}
   }
   
   .detail-content-container {
   	margin-top: 40rpx;
   	// min-height: 1000rpx;
   	.detail-html {
   		padding: 0 30rpx;
   	}
   }
   
   .detail-bottom {
   	position: fixed;
   	bottom: 0;
   	left: 0;
   	@include flex(flex-start);
   	width: 100%;
   	height: 88rpx;
   	border-top: 1px #f5f5f5 solid;
   	background-color: #FFFFFF;
   	box-sizing: border-box;
   	.input-container {
   		@include flex();
   		margin-left: 20rpx;
   		padding: 0 20rpx;
   		flex-grow: 1;
   		height: 60rpx;
   		border: 1px solid #ddd;
   		border-radius: 5px;
   		text {
   			font-size: 28rpx;
   			color: $c-9;
   		}
   	}
   	.detail-bottom-icons {
   		display: flex;
   		flex-shrink: 0;
   		padding: 0 20rpx;
   	}
   	.detail-bottom-icon-box {
   		position: relative;
   		@include flex(center);
   		width: 88rpx;
   	}
   }
   ```

   ## 文章详情页面-数据初始化渲染

   

   ### 一、URL参数处理

   > ​	在listcard组件跳转过程中携带参数到详情界面实现数据与渲染

   ​		**卡片组件**

   ```js
     /* 添加参数传递 */
         const { _id, title, author, create_time, thunbs_up_count, browse_count } = this.item
         const params = { _id, title, author, create_time, thunbs_up_count, browse_count };
         uni.navigateTo({url: `../../pages/articleDetail/articleDetail?params=${JSON.stringify(params)}`})
   ```

   ​        **文章详情界面**

   ```js
   onLoad (...options) {
       this.articleData = JSON.parse(options[0].params)
     },
   ```

   ​		**获取数据后进行UI界面渲染**

   ### 二、进行数据请求发送

   1. 前端携带当前文章ID进行参数传递

   2. 定义云函数

      ```js
      'use strict';
      const db = uniCloud.database();
      exports.main = async (event, context) => {
        const { article_id } = event;
      
        const articleList = await db.collection('article')
          .aggregate()
          .match({
            _id: article_id
          })
          .end();
      
      
      
        //返回数据给客户端
        return {
          code: 0,
          msg: "文章获取成功",
          data: articleList.data[0]
        }
      };
      ```

   3. 获取数据后更新articleData数据

      1. 解析内容数据使用三方插件uParse 

      2. 下载地址：[https://ext.dcloud.net.cn/plugin?id=364](https://ext.dcloud.net.cn/plugin?id=364)

      3. 解析markdown文本使用三方插件marked

         下载：npm install markdown | yarn markdown 

         使用：

         

         ```js
          content () {
               try {
                 return marked(this.articleData.content)
               } catch (e) {
                 return null
               }
             }
         ```




   ## 文章详情页面-评论组件制作

   

   > 当用户为未登录状态，先进行登录界面跳转操作

   ### 一、添加三方插件

   1. 插件市场内下载插件uni-popup 下载地址：[https://ext.dcloud.net.cn/plugin?id=329](https://ext.dcloud.net.cn/plugin?id=329)

   2. 定义弹出层组件CommentMasker，传递是否打开弹窗标识

      ```html
       <CommentMasker  :showPopup="showPopup"></CommentMasker>
      ```

   3. 完成内容区域结构样式创建

      ```css
      <style lang="scss">
      .popup-wrapper {
        background-color: #ffffff;
        .popup-header {
          @include flex();
          font-size: 28rpx;
          color: #666;
          border-bottom: 1px #f5f5f5 solid;
          .popup-header-item {
            height: 100rpx;
            line-height: 100rpx;
            padding: 0 30rpx;
          }
        }
        .popup-content {
          width: 100%;
          padding: 30rpx;
          box-sizing: border-box;
          .popup-content-textarea {
            height: 400rpx;
            width: 100%;
          }
          .popup-content-count {
            @include flex(flex-end);
            font-size: 24rpx;
            color: $c-9;
          }
        }
      }
      </style>
      ```

   二、云函数进行评论内容保存

   1. 前端进行数据收集,获取用户id，文章id，评论内容

   2. 创建云函数,为article进行评论内容追加

      ```
        let commentObj = {
          comment_id: generatedId(5),
          comment_content: content,
          create_time: Date.now(),
          is_reply: false,
          author: {
            author_id: user._id,
            author_name: user.author_name,
            avatar: user.avatar,
            professional: user.professional
          },
          replyArr: []
        }
      
        commentObj = dbCmd.unshift({ commentObj })
        await db.collection('article').doc(articleId).update({
          comments: commentObj
        })
      ```

      ​		为comment_id指定随机id值

      ```js
      function generatedId (num) {
          return Number(Math.random().toString().substr(3, num) + Date.now()).toString(36)
        }
      ```

   3. 返回数据到前端，前端进行弹窗关闭操作

      ```js
         async _sendCommentData (content) {
            const {msg} = await this.$http.update_comment({ articleId: this.articleData._id, userId: this.userInfo._id ,content})
            uni.showToast({
              title:msg,
            })
            this.showPopup = false;
          }
      ```


   ## 文章详情页面-评论展示组件制作

   

   ### 一、界面结构搭建

   > 下载日期格式化组件，下载地址：[https://ext.dcloud.net.cn/plugin?id=3279](https://ext.dcloud.net.cn/plugin?id=3279)

   ### 二、定义云函数，进行内容获取

   1. 前端进行云函数请求

      ```js
       async _getCommentList () {
            const res = await this.$http.get_comments({ articleId: this.formData._id })
          }
      ```

   2. 定义云函数 get_comments 

      ```js
      'use strict';
      const db = uniCloud.database();
      exports.main = async (event, context) => {
        const {
          articleId,
          pageSize = 10,
          page = 1
        } = event;
      
        const list = await db.collection('article')
          .aggregate()
          .match({
            _id: articleId,
          })
          .unwind('$comments') // 从指定的节点进行内容的获取
          .project({
            _id: 0,
            comments: 1
          })
          .replaceRoot({
            newRoot: '$comments'
          })
          .skip(pageSize * (page - 1))
          .limit(pageSize)
          .end()
      
        //返回数据给客户端
        return {
          code: 0,
          msg: '数据请求成功',
          data: list.data
        }
      };
      
      ```

   3. 前端进行内容渲染

      ```js
       <view class="comment-box">
          <view class="comment-header">
            <view class="comment-header-logo">
              <image :src="commentData.author.avatar" mode="aspectFill"></image>
            </view>
            <view class="comment-header-info">
              <view class="title">
                {{commentData.author.author_name}}
              </view>
              <view class="">
                <uni-dateformat :date="commentData.create_time" format="yyyy-MM-dd hh:mm:ss"></uni-dateformat>
              </view>
            </view>
          </view>
          <!-- 内容部分 -->
          <view class="comment-content">
            <view class="">
              {{commentData.comment_content}}
            </view>
            <view class="comment-info">
              <view class="comment-button">
                回复
              </view>
            </view>
          </view>
        </view>
      ```


   ## 文章详情页面-指定评论内容处理

   

   ### 一、指定评论回复按钮点击事件绑定

   1. 添加comment_id传递给云函数，保证云函数知道当前是针对那条评论进行的回复

   ### 二、云函数调整

   1. ​	从当前的commnets集合当中通过传递的comment_id获取指定的那一条记录值

   2. 为当前的记录值的replyArr属性插入一个新的评论内容

      ```js
      // 获取指定的评论内容
      let commentIndex = comments.findIndex(item => item.comment_id === comment_id)
      ```

   3. 修改指定呢索引值的数据的replyArr的记录值

      ```js
      commentObj = {
      			[commentIndex]: {
      				replyArr: dbCmd.unshift(commentObj)
      			}
      		}
      ```

   ### 三、前端进行数据渲染

   > ​	使用组件自调用的形式进行数据渲染

   1. ​	在自调用的过程当中需要注意，保证调用时进行指定name属性值，

   2. 使用自调用的过程中会有两次父组建事件发送的过程，一次是当前组件作为父组件的时候获取到发送的事件，另一次是向上级articleDetail传递的时候接收到的事件。

   3. 当指定回复进行事件发送的时候，需要指定reply_id,并且调整comment_id值；

   4. 渲染完成之后，将replayData进行清空处理

   ## 文章详情页面-关注作者

   

   ### 一、UI显示处理

   > 判断当前的登录用户是否包含文章作者的用户ID

   ```js
   // 添加计算属性 
   isFollowAuthor() {
         return this.userInfo && this.userInfo.author_likes_ids.includes(this.articleData.author.id)
       }
   ```

   ### 二、事件绑定

   > ​	传递文章作者ID，及当前登录用户ID

   ```js
   const { msg } = await this.$http.update_follow_author({ authorId: this.articleData.author.id, userId: this.userInfo._id })
   
   ```

   ### 三、云函数定义

   ```js
   'use strict';
   const db = uniCloud.database();
   const dbCmd = db.command;
   exports.main = async (event, context) => {
     const {
       userId,
       authorId
     } = event;
   
     const user = await db.collection('user').doc(userId).get();
     const authorLikesIds = user.data[0].author_likes_ids
     let returnMsg = ''
   
     let author_ids = null
     if (authorLikesIds.includes(authorId)) {
       returnMsg = '取消关注成功'
       author_ids = dbCmd.pull(authorId)
     } else {
       returnMsg = '关注作者成功'
       author_ids = dbCmd.addToSet(authorId)
     }
   
     // 将处理完的内容进行重新插入
     await db.collection('user').doc(userId).update({
       author_likes_ids: author_ids
     })
   
     //返回数据给客户端
     return {
       code: 0,
       data: {
         msg: returnMsg
       }
     }
   };
   
   ```

   ### 四、前端处理用户保存信息

   ```js
    async _followAuthor () {
         // 用户检测
         await this.checkedIsLogin()
         const { msg } = await this.$http.update_follow_author({ authorId: this.articleData.author.id, userId: this.userInfo._id })
         uni.showToast({
           title: msg,
         })
         //处理用户存储信息
         let followIds = [...this.userInfo.author_likes_ids]
         if (followIds.includes(this.articleData.author.id)) {
           followIds = followIds.filter(item => item != this.articleData.author.id)
         }else {
           followIds.push(this.articleData.author.id)
         }
         this.updateUserInfo({...this.userInfo,author_likes_ids:followIds})
       }
   ```

   ### 五、收藏文章处理

   1. 使用公共组件 SaveLikes

   ```js
     <SaveLikes size="22" class="detail-bottom-icon-box" :item="articleData"></SaveLikes>
   ```

   2. 处理每次请求都进行文章列表加载Bug

## 文章详情页面-点赞+浏览次数实现



### 一、浏览次数操作

> 请求文章详情的云函数返回前端之前进行+1操作

​		

```js
  // 每次请求进行+1操作
  await db.collection('article').update({
	  browse_count:dbCmd.inc(1)
  })
```

### 二、文章点赞UI处理

> ​	使用计算属性进行Ui显示

```js
  isCompliments () {
      try {
        return this.userInfo && this.userInfo.thumbs_up_article_ids.includes(this.articleData._id)
      } catch (e) {
        return false
      }
    }

```

### 三、云函数定义

```js
'use strict';
const db = uniCloud.database()
const dbCmd = db.command  // 使用操作符
exports.main = async (event, context) => {
  const { articleId, userId } = event;

  const userList = await db.collection('user').doc(userId).get();
  const thumbs_up_article_ids = userList.data[0].thumbs_up_article_ids
  let tempArr = null;
  let returnMsg = '';
  let thumbsNumber = null;


  //todo 判断当前用户是否有点赞操作
  if (thumbs_up_article_ids.includes(articleId)) {
    tempArr = dbCmd.pull(articleId)
    thumbsNumber = -1
    returnMsg = '您取消了点赞'
  } else {
    tempArr = dbCmd.addToSet(articleId)
    thumbsNumber = 1
    returnMsg = '点赞成功'
  }

  // 处理用户字段
  await await db.collection('user').doc(userId).update({
    thumbs_up_article_ids: tempArr
  })

  // 处理文章数量字段
  await await db.collection('article').doc(articleId).update({
    thumbs_up_count: dbCmd.inc(thumbsNumber)
  })


  //返回数据给客户端
  return {
    code: 0,
    data: {
      msg: returnMsg
    }
  }
};

```

### 四、前端处理用户保存信息

```js
 // 用户检测
      await this.checkedIsLogin()
      
      const { msg } = await this.$http.update_compliments({ articleId: this.articleData._id, userId: this.userInfo._id })
      msg && uni.showToast({
        title: msg,
      })
      // 修改用户信息
      let thumbsArr = [...this.userInfo.thumbs_up_article_ids]
      if (thumbsArr.includes(this.articleData._id)) {
        this.articleData.thumbs_up_count -= 1
        thumbsArr = thumbsArr.filter(item => item != this.articleData._id)
      } else {
        this.articleData.thumbs_up_count += 1
        thumbsArr.push(this.articleData._id)
      }
      this.updateUserInfo({ ...this.userInfo, thumbs_up_article_ids: thumbsArr })
```

评论页面制作



### 一、页面注册

1. 创建页面
2. page.json中进行页面注册		
3. 跳转页面时携带指定的文章ID

### 二、结构样式编写

1. 使用评论组件

   ```js
    <view class="comment-content-container" v-for="item in commentList" :key="item.comment_id">
         <CommentBox @commnetReply="commnetReply" :commentData="item"></CommentBox>
       </view>
   ```

   2. 使用uni-load-more组件，对组件内部初始化属性进行调整操作

      ```js
       <uni-load-more v-if="commentList.length===0 || commentList.length > 5" :status="loading" :contentText="{	contentdown: '上拉显示更多',
      						contentrefresh: '正在加载...',
      						contentnomore: '没有更多评论了'}"></uni-load-more>
      ```

   3. 根据条件进行评论列表的追加操作

      ```js
       async _getCommentList () {
            const list = await this.$http.get_comments({
              articleId: this.articleId,
              page: this.page,
              pageSize: this.pageSize,
            })
            if (list.length === 0) {
              this.loading = 'noMore'
              return
            }
            let oldList = JSON.parse(JSON.stringify(this.commentList))
            oldList.push(...list)
            this.commentList = oldList
          },
      ```

### 三、添加评论内容输入组件

```js
 <!-- 评论内容输入组件 -->
    <CommentMasker :showPopup="showPopup" @closePopupMasker="showPopup=$event" @sendCommentData="_sendCommentData">
    </CommentMasker>
```

### 四、处理评论发布业务

1. 回复事件函数处理

   ```js
     /* 处理回复事件函数 */
       commnetReply (data) {
         this.replyData = {
           "comment_id": data.comment.comment_id,
           is_reply: data.isReply
         }
         // 当前为回复内容的时候添加回复的ID
         data.comment.reply_id && (this.replyData.reply_id = data.comment.reply_id)
         this.openMaskerComment()
       },
   ```

2. 副作用事务处理

   ```js
       async _sendCommentData (content) {
         const {
           msg
         } = await this.$http.update_comment({
           userId: this.userInfo._id,
           articleId: this.articleId,
           content,
           ...this.replyData   // 扩展当前是否为回复指定评论内容
         })
         uni.showToast({
           title: msg
         })
         // 处理副作用事物
         this.showPopup = false;
         this.replyData = {};
         this.page = 1;
         this.commentList = [];
         this._getCommentList();
       }
   ```

## 关注界面-结构搭建

### 添加路由守卫

1. 三方插件使用

   文档地址：[https://hhyang.cn/v2/](https://hhyang.cn/v2/)

2. 进行守卫规则添加

   ```js
   //全局路由前置守卫
   router.beforeEach((to, from, next) => {
     // 判断当前页面是否需要登录并且现在是没有登录的状态
     if (to.meta.needLogin && !store.state.userInfo) {
       next({
         name: "login",
         NAVTYPE: "push"  //跳转到普通页面，新开保留历史记录
       })
     } else {
       next();
     }
   });
   ```

3. 调整路由条装方式为绝对路径

   ```js
   // listCard处理路径跳转
         uni.navigateTo({url: `/pages/articleDetail/articleDetail?params=${JSON.stringify(params)}`})
   
   ```

   4. article内调整路由接收方式

      ```js
       this.articleData = this.$Router.currentRoute.query.params
      ```

   5. 处理小程序无法兼容问题

      ```js
        // #ifdef MP-WEIXIN
      		if(!this.$store.state.userInfo) {
      			uni.redirectTo({
      				url:'/pages/userInfo/login/login'
      			})
      			return 
      		}
            // #endif
      ```

### 二、界面结构样式搭建

​			

```js
<view class="follow-container">
    <view class="follow-tab">
      <view class="follow-tab-box">
        <view class="follow-tab-item" :class="{active:currentIndex===0}">文章</view>
        <view class="follow-tab-item" :class="{active:currentIndex===1}">作者</view>
      </view>
    </view>
    <!-- 内容切换区域 -->
    <view class="follow-list-container">
      <swiper class="follow-list-swiper" :current="currentIndex">
        <swiper-item>
          <ListItem :isShowLoading="isShowLoading" :articleList="articleList" v-if="articleList.length"></ListItem>
          <view v-if="dataNone"  class="no-data">暂无收藏的文章</view>
        </swiper-item>
        <swiper-item>
          2
        </swiper-item>
      </swiper>
    </view>
  </view>
```

### 三、云函数定义

```js
'use strict';
const db = uniCloud.database()
const $ = db.command.aggregate; // 获取一个聚合的操作符

exports.main = async (event, context) => {
	const {
		userId
	} = event;

	let userInfo = await db.collection('user').doc(userId).get()
	let article_likes_ids = userInfo.data[0].article_likes_ids; // 获取用户的收藏文章的数组

	const list = await db.collection('article')
		.aggregate()
		.addFields({
			// 判断这个文章的数组是否包含文章的_id ,$_id 指的是文章列表里面的_id,如果包含，返回true，否则，返回false，在这个里面是过滤查询的每一条记录值
			is_like: $.in(['$_id', article_likes_ids])
		})
		.project({
			content: 0
		})
		.match({
			is_like:true
		})
		.end();

	//返回数据给客户端
	return {
		code: 0,
		msg: "请求成功",
		data: list.data
	}
};

```

## 关注界面-作者组件制作

### 一、全局事件监听

> ​		处理关注界面数据不刷新问题，使用uni.$emit事件注册全局事件

```js
     // saveLike组件
     uni.$emit('updateArticle')

    // followPage界面

  // todo 没有这个历史记录栈的时候不会触发这个事件
    uni.$on('updateArticle',(e)=> {
      this._getFollowArticle();
    })
```

### 二、作者组件结构搭建

1. 关联swiper滑动组件
2. 结构样式添加   

### 三、云函数定义

```js
'use strict';
const db = uniCloud.database()
const $ = db.command.aggregate; // 获取一个聚合的操作符

exports.main = async (event, context) => {
	const {
		userId
	} = event;

	let userInfo = await db.collection('user').doc(userId).get()
	let article_likes_ids = userInfo.data[0].article_likes_ids; // 获取用户的收藏文章的数组

	const list = await db.collection('article')
		.aggregate()
		.addFields({
			// 判断这个文章的数组是否包含文章的_id ,$_id 指的是文章列表里面的_id,如果包含，返回true，否则，返回false，在这个里面是过滤查询的每一条记录值
			is_like: $.in(['$_id', article_likes_ids])
		})
		.project({
			content: 0
		})
		.match({
			is_like:true
		})
		.end();

	//返回数据给客户端
	return {
		code: 0,
		msg: "请求成功",
		data: list.data
	}
};

```

### 四、客户端渲染

> ​	将获取到的内容进行渲染操作

### 五、数据同步

​		定义全局事件，实现修改关注作者时触发foll_author事件从新调用

```js
uni.$on('updateAuthor',(e)=> {
      this._getAuthorList();
    })
```

## 个人中心-页面结构搭建

### 一、未登录状态

1. 展示未登录提示结构；
2. 在未登录状态下可实现界面跳转

### 二、登录状态

1. 展示用户登录信息内容
2. 添加退出按钮，定义退出函数

## 个人中心-我的文章

### 一、进行用户信息渲染

### 二、完成app升级版本逻辑处理

1. 初始化onLoad事件进行版本检测

   ```js
     // !判断是否有新版本进行下载及获取当前的版本
       // #ifdef APP-PLUS
       uni.getSystemInfo({
         success: (res) => {
           if (res.platform == "android") {
             plus.runtime.getProperty(plus.runtime.appid, wgtinfo => {
               this.currentVersion = wgitinfo;
               this._checkVersion();
             })
           }
         }
       })
       // #endif
   ```

2. 进行版本检测，判断当前版本是否小于最新版本

   ```js
    // app中判断是否有新版本
       async _checkVersion() {
         const {version,downLoadLinkUrl} = await this.$http.get_current_version();
         if(version > this.currentVersion) {
           this.haveNewVersion = true;
           this.downLoadLinkUrl = downLoadLinkUrl
         }
       },
   ```

   

3. 下载最新版本内容进行安装处理

   ```js
    // 获取最新版本app下载
       _getNewVersion() {
         uni.showLoading({title:'下载中，请稍后'});
          var dtask = plus.downloader.createDownload(this.downLoadLinkUrl, {}, function (d, status) {
           // 下载完成  
           uni.hideLoading({})
           if (status == 200) {
             plus.runtime.install(plus.io.convertLocalFileSystemURL(d.filename), {}, {}, function (error) {
               uni.showToast({
                 title: '安装失败',
                 duration: 1500,
                 icon: 'none'
               });
             })
           } else {
             uni.showToast({
               title: '更新失败',
               duration: 1500,
               icon: 'none'
             });
           }
         });
         dtask.start();
       }
   ```

### 三、我的文章处理

1. 创建页面

2. 组件引入

3. 数据获取-云函数定义

   ```js
   ## 个人中心-意见反馈
   
   ### 一、页面结构搭建
   
   1. 结构创建
   
   2. 样式处理
   
      ```css
      .feedback-title {
          margin: 30rpx;
          margin-bottom: 0;
          font-size: 28rpx;
          color: #666;
      }
      
      .feedback-content {
          margin: 30rpx;
          padding: 20rpx;
          box-sizing: border-box;
          border: 1px solid #eee;
          .feedback-textarea {
              font-size: 24rpx;
              width: 100%;
              height: 200rpx;
          }
      }
      
      .feedback-image-box {
          display: flex;
          flex-wrap: wrap;
          padding: 20rpx;
          .feedback-image-item {
              position: relative;
              width: 33.33%;
              height: 0;
              padding-top: 33.33%;
              box-sizing: border-box;
              .close-icon {
                  @include flex(center);
                  right: 0;
                  top: 0;
                  width: 44rpx;
                  height: 44rpx;
                  position: absolute;
                  border-radius: 50%;
                  z-index: 2;
                  background-color: $base-color;
              }
              .image-box {
                  @include flex(center);
                  top: 10rpx;
                  right: 10rpx;
                  bottom: 10rpx;
                  left: 10rpx;
                  border: 1px solid #eee;
                  border-radius: 10rpx;
                  overflow: hidden;
                  position: absolute;
                  image {
                      width: 100%;
                      height: 100%;
                  }
              }
          }
      }
      
      .feedback-button {
          margin: 0 30rpx;
          background-color: $base-color;
      }
   ```
   
   ### 二、新增图片操作
   
   1. chooseImage参考地址：[https://uniapp.dcloud.io/api/media/image?id=chooseimage](https://uniapp.dcloud.io/api/media/image?id=chooseimage)
   
   2. 为前端UI进行图片定义
   
      ```js
        const count = 5 - this.imageList.length;
            uni.chooseImage({
              count,
              success: res => {
                const tempFilePaths = res.tempFilePaths;
                tempFilePaths.forEach((url, index) => {
                  if (index < count) {
                    this.imageList.push({
                      url,
                      name: res.tempFiles[index].name
                    })
                  }
                })
              }
            })
      ```
   
      
   
   ### 三、发送数据到云函数
   
   1. 图片直传参考地址：[https://uniapp.dcloud.io/uniCloud/storage?id=clouduploadfile](https://uniapp.dcloud.io/uniCloud/storage?id=clouduploadfile)
   
   2. 收集图片上传成功之后的访问地址
   
      ```js
       return this.imageList.map(item => {
              return new Promise(async resolve => {
                const result = await uniCloud.uploadFile({
                  filePath: item.url,
                  cloudPath: item.name
                })
                resolve(result.fileID)
              })
            })
      ```
   
   3. 定义云函数
   
      ```js
      'use strict';
      const db = uniCloud.database();
      exports.main = async (event, context) => {
      	const {
      		userId,
      		feedbackImageList,
      		content
      	} = event
      	
      	await db.collection('feedback').add({
      		user_id:userId,
      		feedbackImageList,
      		content
      	})
      	return {
      		code:0,
      		data:{
      			msg:"提交反馈成功"
      		}
      	}
      };
      ```
   
   ### 四、用户头像修改
   
   > ​		获取修改头像内容，上传云函数 ，进行图片的修改，及原图片的删除操作
   
   ```js
   'use strict';
   const db = uniCloud.database();
   exports.main = async (event, context) => {
   	const {
   		userId,
   		filePath
   	} = event;
   	
   	const user = await db.collection('user').doc(userId).get()
   	const oldImgList = user.data[0].avatar
   	try {
   		await uniCloud.deleteFile({
   			fileList: [oldImgList],
   		});
   	}catch(e) {
   		console.log(e)
   	}
   	 
   	 await db.collection('user').doc(userId).update({
   		avatar:filePath
   	})
   	
   	//返回数据给客户端
   	return {
   		code: 0,
   		data: {
   			msg:"修改头像成功",
   		}
   	}
   };
   
   ```
   
   ​			
   
   'use strict';
   const db = uniCloud.database()
   const dbCmd = db.command;
   
   exports.main = async (event, context) => {
   	const {
   		userId
   	} = event;
   
   	let userInfo = await db.collection('user').doc(userId).get()
   	let article_ids = userInfo.data[0].article_ids; 
   	
   	const list = await db.collection('article')
   		.aggregate()
   		.project({
   			content: 0,
   			comments:0
   		})
   		.match({
   			id:dbCmd.in(article_ids)
   		})
   		.end();
   	
   	//返回数据给客户端
   	return {
   		code: 0,
   		msg: "请求成功",
   		data: list.data
   	}
   };
   
   ```
   
   ```

## 发布-wap端发行打包

> 打包参考地址：[https://uniapp.dcloud.io/collocation/manifest?id=h5](https://uniapp.dcloud.io/collocation/manifest?id=h5)

![image-20230213120022226](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131200409.png)

#### unicloud网页托管配置

> 使用unicloud前端网页托管的话需要进行安全域名配置

参考地址：[https://uniapp.dcloud.io/uniCloud/hosting](https://uniapp.dcloud.io/uniCloud/hosting)

## 发布-微信小程序发布

> 打包参考地址：[https://uniapp.dcloud.io/collocation/manifest?id=h5](https://uniapp.dcloud.io/collocation/manifest?id=h5)

1. 打包配置文件

   - 获取小程序ID；

   - 进行安全域名配置

     ![image-20230213133221370](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131332504.png)

2. 小程序发布

3. 提交预发布版本

4. 提交审核

   参考地址：https://mp.weixin.qq.com/wxamp/wacodepage/getcodepage?token=1374043880&lang=zh_CN

## 发布-app安卓系统应用打包发布

### 一、配置

1. 基础配置

   ![image-20230213133412430](https://duyi-bucket.oss-cn-beijing.aliyuncs.com/uni/202302131334590.png)

2. 图标使用

   > 使用1024*1024图标

3. 其他配置暂时忽略

### 二、证书下载

> 证书下载地址：[https://www.taomamao.cn/index.php/apkcert](https://www.taomamao.cn/index.php/apkcert)
