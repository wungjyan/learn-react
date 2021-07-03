## 介绍

几年前学过 React ，但是一直没有在工作中用上，这次准备重学一遍，以后有机会要在工作中用上。

关于 React 的介绍这里就不多描述，比如什么 `虚拟DOM` 之类的概念，也不会详说，这里纯记录学习过程。

## 编写 React 代码

实际工作中基本使用 React 脚手架去开发，但初学阶段我们可以直接使用 `script` 标签引入 React 相关库文件来开发，这便于我们理解 React 开发需要用到哪些东西。不同于使用 Vue，你只需要引入 `vue.js` 库文件即可，使用 React 时，需要用到两个基本库，即 `react.js` 和 `react-dom.js`。

html 代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React Demo</title>
</head>
<body>
    <!-- react 应用的容器 -->
    <div id="test"></div> 

    <!-- 引入 react 核心库 -->
    <script src="https://unpkg.com/react@17/umd/react.production.min.js" crossorigin></script>
  
    <!-- 引入 react-dom，支持 React 操作 DOM -->
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js" crossorigin></script>

    <script>
       // 使用 React.createElement 创建虚拟 DOM
       const VDOM = React.createElement('div',{},'hello,world!')
       // 将虚拟 DOM 渲染到容器里
       ReactDOM.render(VDOM,document.getElementById('test'))
    </script>
</body>
</html>
```

上述代码演示了使用 React 开发的一个基本过程：

1. 首先 React 应用需要挂载到页面的一个容器上，所以我们需要定义一个最外层的容器，即代码中的 `<div id="test"></div>`；
2. 开发 React 应用需要用到两个基本库，即 `react.js` 和 `react-dom.js` ，前者是核心库，暴露全局变量 `React`，后者是提供 DOM 操作相关功能，暴露全局变量 `ReactDOM`；
3. 使用 React 构建页面，其实就是在写虚拟 DOM，可以使用提供的 `React.createElement` 方法来创建虚拟DOM，然后调用 `ReactDOM.render`方法来将虚拟 DOM 渲染成真实 DOM，挂载到容器上。这样就能在浏览器上看到所编写内容。



## 使用 JSX 

上面说到使用 React 编写界面，其实就是在写虚拟 DOM，而创建虚拟 DOM 是使用 `React.createElement` 这个方法的，但实际开发中是不会直接使用这个方法的，因为特别不方便。比如我们要写一个这样 DOM 结构：

```html
<div>
  <h1 id="title">你好</h1>
</div>
```

如果使用创建虚拟DOM方法来写，就得这样：

```js
const VDOM = React.createElement('div',{},React.createElement('h1',{id:'title'},'你好'))
```

显然易见，这样是很麻烦的，尤其是真实开发中的页面代码都是成千上万的，没有办法这样一直嵌套写下去，所以 React 创造出了 `JSX` 这样的神器，便于我们编写页面DOM代码。



需要注意的是，我们的浏览器是不认识 `JSX` 语法的，我们需要对它进行转换，可以使用 `babel` 这个插件来转译代码。使用` JSX` 开发：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React JSX Demo</title>
</head>
<body>
    <!-- react 应用的容器 -->
    <div id="test"></div> 

    <!-- 引入 react 核心库 -->
    <script src="https://unpkg.com/react@17/umd/react.production.min.js" crossorigin></script>
    <!-- 引入 react-dom，支持 React 操作 DOM -->
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js" crossorigin></script>

    <!-- 引入 babel，用来转转译 JSX 语法 -->
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

    <!-- 注意：这里的 type 要写成 text/babel -->
    <script type="text/babel">
       // 编写 JSX 代码
       const VDOM = <div><h1 id="title">你好</h1></div>
       // 将虚拟 DOM 渲染到容器里
       ReactDOM.render(VDOM,document.getElementById('test'))
    </script>
</body>
</html>
```

首先需要引入 `babel` 插件，需要注意的是实际开发中不应该这么引入，因为这样浏览器会实时转换`JSX`代码，影响性能，我们这里只是为了演示 JSX 开发。

然后需要在编写逻辑代码的 `script` 标签上加上 `type="text/babel">`，不指定类型的话，浏览器是无法转译 JSX 代码的。

JSX 其实跟我们编写 Vue 中的 `template` 类似的，你可以理解为是在我们熟悉的 html 代码上做一些特有的定制化，就成了 JSX，个人觉得没有学习成本的负担。后面会单独介绍 JSX 相关知识。

