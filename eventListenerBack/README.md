常使用的场景：移动前端  
&emsp;&emsp;1、安卓手机物理返回键  
&emsp;&emsp;2、苹果手机在企业微信打开浏览器的返回按钮

移动前端开发语言是：vue  
&emsp;&emsp;路由跳转：vue-router hash模式

先介绍一下html5中history有哪些属性和API，我们用到了其中2个方法（pushState、replaceState），来根据状态存储的数据判断是否触发返回事件  
&emsp;&emsp;1、window.history.length - 历史记录长度  
&emsp;&emsp;2、window.history.state - 历史记录状态  
&emsp;&emsp;3、window.history.go(num) - 回到指定的历史记录（参数num可以是正/负）  
&emsp;&emsp;4、window.history.back() - 回到上一个历史记录  
&emsp;&emsp;5、window.history.forward() - 回到下一个历史记录（前提当前历史记录不是最新的）  
&emsp;&emsp;6、window.history.pushState(state, title, newUrl) - 新增一个历史记录（路径等于当前的url + newUrl ）  
&emsp;&emsp;7、window.history.replaceState(state, title, newUrl) - 替换当前的历史记录路径（路径等于当前的url + newUrl ）  

监听事件：window.onpopstate

**pushState和replaceState作用演示：**
&emsp;&emsp;打开当前页面路径如下(D:/webstorm_workspace/demo-code/eventListenerBack/test.html)，历史记录长度1  

点击pushState按钮：创建了一条新的历史记录（新建状态）、历史记录长度2  

在这里插入图片描述

pushState按钮的代码如下：
```js
// pushState会新建一条历史记录
pushState = () => {
  let state = {'name': '张三 - pushState'}
  window.history.pushState(state, null, '?pushState')
  console.log('pushState')
  console.log(window.history.state)
}
```
点击replaceState按钮：替换当前的历史记录（更新状态），历史记录长度2
在这里插入图片描述

replaceState按钮的代码如下：
```js
// replaceState会覆盖当前的历史记录
replaceState = () => {
  let state = {'name': '张三 - replaceState'}
  window.history.replaceState(state, null, '?replaceState')
  console.log('replaceState')
  console.log(window.history.state)
}
```

#### 监听事件演示
&emsp;&emsp;点击返回按钮：会触发监听事件window.onpopstate方法；之前的路径是(D:/webstorm_workspace/demo-code/eventListenerBack/test.html?replaceState)，返回到(D:/webstorm_workspace/demo-code/eventListenerBack/test.html)
在这里插入图片描述

返回按钮的代码如下：
```js
// 返回按钮监听
window.onpopstate = (e) => {
  console.log('触发onpopstate方法')
  console.log(historyState)
  // 判断前一个历史记录存储的state数据来确定是否需要改变当前的数据
}
```

#### 总结
&emsp;&emsp;1、什么时候会触发这个监听事件？除了back方法，go和forward方法也可以触发  
&emsp;&emsp;2、前进后退历史记录需要根据条件判断时，需要绑定监听事件  
