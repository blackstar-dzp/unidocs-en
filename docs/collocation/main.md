`main.js`是uni-app的入口文件，主要作用是初始化`vue`实例、定义全局组件、使用需要的插件如vuex。
`main.js`It is the entry file of uni-app. Its main function is to initialize `vue`instances, define global components, and use required plug-ins such as vuex.

首先引入了`Vue`库和`App.vue`，创建了一个`vue`实例，并且挂载`vue`实例。
First introduced the `Vue`library and `App.vue`, created an `vue`instance, and mounted the `vue`instance.
```
import Vue from 'vue'
import App from './App'
//全局引用page-head组件
//Global reference to the page-head component
import pageHead from './components/page-head.vue'

Vue.config.productionTip = false
//全局注册page-head组件，每个页面将可以直接使用该组件
//Globally register the page-head component, which each page will be able to use directly
Vue.component('page-head', pageHead)
App.mpType = 'app'

const app = new Vue({
    ...App
})
//挂载Vue实例
//Mount the Vue instance
app.$mount()
```
使用`Vue.use`引用插件，使用`Vue.prototype`添加全局变量，使用`Vue.component`注册全局组件。
Use `Vue.use`reference plugins, use `Vue.prototype`add global variables, and use `Vue.component`register global components.

可以引用`vuex`，因涉及多个文件，此处没有提供示例，详见`hello uni-app`示例工程。
It can be cited `vuex`, because multiple files are involved, no examples are provided here, please refer to the `hello uni-app`example project for details .

无法使用`vue-router`，路由须在`pages.json`中进行配置。如果开发者坚持使用`vue-router`，可以在[插件市场](https://ext.dcloud.net.cn/search?q=vue-router)找到转换插件。
Cannot be used `vue-router`, routing must `pages.json`be configured in. 


**注意**
**note**
- nvue 暂不支持在 main.js 注册全局组件
- nvue does not currently support registering global components in main.js
