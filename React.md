## React的生命周期
![React的生命周期](https://user-images.githubusercontent.com/14359831/55124486-53abc180-5141-11e9-95c0-4a3d8d5c2e55.png)

### 有没有自己写过组件？如何实现样式法继承和复用

React的脚手架有哪些：Create-React-App(CRA) 

Create-React-App是官方推出的脚手架





React的项目目录结构：

public:

src:

1. components
   1. container
      1. actions
      2. store
      3. xxxx.js
      4. 



React的路由：

使用React-Router 4.0

官网：https://reacttraining.com/react-router/web/example/basic





前端mock数据的一把思路：

1. 后台搭建一个express或者koa等node服务器(mock server)，自己在里面模拟数据，前端使用ajax获取
2. 前端设置一个mock文件夹，将数据以js的形式mock
3. 使用开源工具yapi，地址->这里，easy-mock或者阿里的RAP2




React-Route 4.0    

官网：https://reacttraining.com/react-router/web/example/basic





組件是React強大的声明式編程模型的核心。React Router是一组导航组件，它们与您的应用程序以声明方式组合。无论您是希望为Web应用程序设置可收藏的URL还是为React Native提供组合式导航，React Router都可以在React渲染的任何地方工作 - 所以请选择它！



基本的组件：

router组件，路由匹配组件和导航组件

1. router组件：

react-router-dom 提供<BrowserRouter> 和<HashRouter> ，他们都能够创建history对象存储路由的跳转记录。

1. 路由匹配组件

路由匹配组件有 <Route> 和<Switch> 

1. 导航组件

React Router提供Link组件，NavLink组件是一种特殊的Link组件，只要当前location匹配，就会自动进入active状态，Redirect组件是一个强制跳转组件，例如用户退出登录等等。





V4.0 和V3.0的区别？






为什么Juery会被取代？三大框架解决了哪些问题？



Vue2.0和3.0分别是如何实现双向绑定的？



React的diff算法





路由机制的原理



Vue的nexttick的实现原理
