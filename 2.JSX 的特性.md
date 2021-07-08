JSX 写起来很像在写 html，但这两个完全不是一个东西。JSX 其实算是 JS 的一种扩展语法，最终会转换成一个虚拟 DOM 的对象。

## 不要用引号

最容易犯的错误就是用引号来包裹 JSX 语句，就像这样：

```js
const dom = "<p>hello world</p>"
```

这样写的话其实还是受 js 的写法影响，JSX 并不是字符串，如果写成字符串的话，React 就不能生成虚拟 DOM 了，从而不能渲染成最终的人 html 标签。

## 需要一个根元素

```jsx
<div>
	<p>aaaaaa</p>
  <p>bbbbbb</p>
	<div>
  		<p>hello</p>
  </div>
</div>
```

如上，在最外层需要包裹一个根元素，这跟 vue 中的 `template`是一样的。不过 vue3 已经支持多个根元素了。

## 表达式要用 { } 包裹

JSX 中插入变量时，需要用 `{}` 包裹，注意 `{}` 中需要使用 js 表达式，不是所有的 js 语句都能生效的。区分是不是表达式的方法就是是否可以赋值给一个变量。比如渲染一个列表，可以这样：

```jsx
const arr = ['Vue','React','Angular']
const VDOM = (
  <ul>
    {arr.map(item=><li>{item}</li>)}
  </ul>
)
ReactDOM.render(VDOM,document.getElementById('test'))
```

可以使用 `map`，但不能使用 `for` 、`forEach` 等循环语句，因为不是 js 表达式。

## 标签类名要用 className

JSX 里要写类名时，不能用 `class`，而是要用 `className`：

```jsx
<h1 className="title"></h1>

// 这样时错误的
<h1 class="title"></h1>
```

始终记住，JSX 并不是等同 html，因为 `class` 是 js 中的关键字，为了避免冲突，类名定义需要使用 `className`

## 内联 style 需要使用 {{ }}

内联样式，需要使用 `{{}}` 包裹，如下：

```jsx
<p style={{color:'red'}}></p>
```

`{{}}` 的外层 `{}` 就是上面说到的表达式需要使用这个符号包裹，而内部的 `{}` 其实就是对象，这个对象是采用小驼峰命名属性的，像是 `font-size` 这样的样式，需要这样写：

```jsx
<p style={{fontSize:'15px'}}></p>
```

## 标签必须闭合

JSX 中的标签必须严格闭合，尤其是一些自闭和标签也不要忘记闭合，如：

```jsx
<img src="" />
<input />
```

## 自定义标签

除了浏览器能识别的 html 标签，有时我们也会写出一些自定义标签。JSX 在处理这些标签时，会根据标签的首字母大小写来进行不同操作：

1. 若标签首字母是小写的，JSX 会将该标签转化为 html 中的同名标签，若 html 中不存在该同名标签，会正常显示内容，但会提示不规范；
2. 若标签首字母是大写的，React 会将它当作一个组件渲染，若没有此组件，就会报错。

