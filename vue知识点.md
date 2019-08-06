### 安装

1.安装
> npm install vue -- ( 安装vue )

2.创建项目 

( vue-cli 2.x.x版本 )

> npm install -g vue-cli -- ( 全局安装vue-cli )

> vue init webpack [program-name] -- ( 创建一个基于webpack的项目 )
 
( vue-cli 3.0 版本)

> vue create [program-name] -- ( 之后按照提示手动选择需要的各种安装包 )

3.进入项目，安装并运行

> cd [program-name] -- ( 进入项目文件夹 )

> npm install -- ( 初始化项目，安装依赖 )

> npm run dev -- ( 运行项目 )

4.在浏览器访问 http://localhost:8080

### 生命周期

![生命周期](https://cn.vuejs.org/images/lifecycle.png)

1. beforeCreate 

	在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。
	
2. created 

	在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。
	
3. beforeMount 

	在挂载开始之前被调用：相关的 render 函数首次被调用。
	
	该钩子在服务器端渲染期间不被调用。
	
4. mounted 

	el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。
	
	该钩子在服务器端渲染期间不被调用。
	
5. beforeUpdate

	数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。
	
	该钩子在服务器端渲染期间不被调用，因为只有**初次渲染**会在服务端进行。
	
6. updated

	由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。

	当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态。如果要相应状态改变，通常最好使用计算属性或 watcher 取而代之。
	
	该钩子在服务器端渲染期间不被调用。
	
7. beforeDestroy

	实例销毁之前调用。在这一步，实例仍然完全可用。

	该钩子在服务器端渲染期间不被调用。
	
8. destroyed

	Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

	该钩子在服务器端渲染期间不被调用。

### vue几种常用的指令

1. v-if

2. v-show

3. v-bind

4. v-on

5. v-for

6. v-model

7. v-text

### v-if 与 v-show 的区别

相同点：v-if 与 v-show 都可以动态控制dom元素显示隐藏

不同点：v-if 对dom元素进行添加或删除的操作

       v-show 通过为该元素添加display:none来实现隐藏显示
	   
### 父子组件间的传递方法

父传子：子组件通过 props 获取数据

子传父：子组件通过 $emit 传递数据

### 路由的钩子函数

1. 全局钩子函数

```
Vue.beforeEach(function(to,form,next){})  /*在跳转之前执行*/
Vue.afterEach(function(to,form){}) /*在跳转之后判断*/
```

全局钩子函数在入口文件main.js中定义

```
router.beforeEach((to, from, next) => {
    let token = router.app.$storage.fetch("token");
    let needAuth = to.matched.some(item => item.meta.login);
    if(!token && needAuth) return next({path: "/login"});
    next();
});
//判断是否有token,如果有，则说明保持着登录状态，如果没有，则要重新登录
```

to:router即将进入的路由对象

from:当前导航即将离开的路由

next:Function,进行管道中的一个钩子，如果执行完了，则导航的状态就是 confirmed （确认的）；否则为false，终止导航。

afterEach函数不用传next()函数。

2. 单个路由里面的钩子

主要用于写某个指定路由跳转时需要执行的逻辑.

```
{
	path: '/news',
	component: resolve => require(['../components/page/news.vue'], resolve),
	meta: { title: '新闻' }
},

```

3. 组件路由

主要包括 beforeRouteEnter(to, from, next){} 和 beforeRouteUpdate(to, from, next){} , beforeRouteLeave(to, from, next){}





