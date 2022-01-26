---
title: "Learn React 01"
date: 2022-01-26T13:34:02+08:00
draft: false
tags: [React]
categories: [React]
---

> React  基础语法

#### 1、万物皆可HelloWorld

```jsx
// 1.创建虚拟DOM
const VDOM = <h1>HelloWorld<h1/>    
// 2.渲染虚拟DOM到页面
ReactDOM.render(VDOM,document.getElementById('app'))
```

完整代码：[HelloWorld](https://github.com/zhishouH/learn-react/blob/main/react-basic/01-hello-world/index.html)

#### 2、虚拟DOM的两种创建方式

- 使用jsx创建虚拟DOM

  ```jsx
  // 1.创建虚拟DOM
  const VDOM = (
    <h1 id="title">
        <span>hello react</span>
    </h1>
  )
  // 2.渲染虚拟DOM到页面
  ReactDOM.render(VDOM, document.getElementById('app'))
  ```

  完整代码：[使用jsx创建虚拟DOM](https://github.com/zhishouH/learn-react/blob/main/react-basic/02-%E8%99%9A%E6%8B%9FDOM%E7%9A%84%E4%B8%A4%E7%A7%8D%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F/1-%E4%BD%BF%E7%94%A8jsx%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9FDOM.html)

- 使用js创建虚拟DOM

  ```js
  // 1.创建虚拟DOM
  const VDOM = React.createElement('h1', { id: 'title' }, 'hello react')
  // 2.渲染虚拟DOM到页面
  ReactDOM.render(VDOM, document.getElementById('app'))
  ```

  完整代码：[使用js创建虚拟DOM](https://github.com/zhishouH/learn-react/blob/main/react-basic/02-%E8%99%9A%E6%8B%9FDOM%E7%9A%84%E4%B8%A4%E7%A7%8D%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F/2-%E4%BD%BF%E7%94%A8js%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9FDOM.html)

- 虚拟DOM和真实DOM：

  虚拟DOM本质上是Object类型的对象(一般对象)

  虚拟DOM比较“轻”，真实DOM比较“重”，因为虚拟DOM是React内部在用，无需真实DOM上那么多的属性

  虚拟DOM最终会被React转化为真实DOM，呈现在页面上

  完整代码：[虚拟DOM和真实DOM](https://github.com/zhishouH/learn-react/blob/main/react-basic/02-%E8%99%9A%E6%8B%9FDOM%E7%9A%84%E4%B8%A4%E7%A7%8D%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F/3-%E8%99%9A%E6%8B%9FDOM%E5%92%8C%E7%9C%9F%E5%AE%9EDOM.html)

#### 3、jsx语法规则

```jsx
const myId = "title"
const myData = "hello-World"
// 1、创建虚拟dom
const VDOM = (
  <h2 className="vdom" id={myId}>
     <span style={{ color: "tomato ", fontSize: "40px" }}>{myData}</span>
  </h2>
)
// 2、渲染到页面
ReactDOM.render(VDOM, document.getElementById('app'))
```

- 1、定义虚拟dom时，不要写引号

-  2、标签中混入js表达式要用{}

- 3、样式中的类名不要用class,要用className

- 4、内联样式要用style={{key:value,key:value}}的形式

- 5、只能有一个根标签

- 6、标签要闭合  

- 7、标签首字母

  ​		小写字母开头，则将该标签转为html中同名元素，若html中无对应的则报错

  ​		大写字母开头，react渲染对应的组件，若组件未定义则报错

完整代码：[jsx语法规则](https://github.com/zhishouH/learn-react/blob/main/react-basic/03-jsx%E8%AF%AD%E6%B3%95%E8%A7%84%E5%88%99/index.html)

#### 4、组件定义

- 函数式组件

  ```jsx
  // 1、创建函数式组件
  function MyComponent() {
    return (
      <h2>函数定义的组件</h2>
    )
  }
  // 2、渲染组件到页面
  ReactDOM.render(<MyComponent />, document.getElementById('app'))
  ```

  完整代码：[函数式组件](https://github.com/zhishouH/learn-react/blob/main/react-basic/05-react%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6/1-%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BB%84%E4%BB%B6.html)

- 类式组件

  ```jsx
  // 1、创建类式组件
  class MyComponent extends React.Component {
    render() {
      console.log("render中的this", this);
      return (
        <h2>类式组件</h2>
      )
    }
  }
  // 2、渲染组件到页面
  ReactDOM.render(<MyComponent />, document.getElementById('app'))
  
  ```

  完整代码：[类式组件](https://github.com/zhishouH/learn-react/blob/main/react-basic/05-react%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6/2-%E7%B1%BB%E5%BC%8F%E7%BB%84%E4%BB%B6.html)

#### 5、组件实例属性——state

```jsx
class MyComponent extends React.Component {
  state = { isHot: true }
  render() {
    const { isHot } = this.state
    return (
      <h1 onClick={this.changeWeather}>今天天气很{isHot ? '炎热' : '凉爽'}</h1>
    )
  }
  changeWeather = () => {
    const { isHot } = this.state
    this.setState({ isHot: !isHot })
  }
}

ReactDOM.render(<MyComponent />, document.getElementById('app'))
```

完整代码：[组件实例属性——state](https://github.com/zhishouH/learn-react/tree/main/react-basic/06-%E7%BB%84%E4%BB%B6%E5%AE%9E%E4%BE%8B%E4%B8%89%E5%A4%A7%E5%B1%9E%E6%80%A7-state)

#### 6、组件实例属性——props

```jsx
class Person extends React.Component {
// 构造器是否接收 props,是否传递props，却决于是否希望在构造器中通过this访问props
// constructor(props) {
//   console.log(props);
//   super(props)
// }
  static propTypes = {
    name: PropTypes.string.isRequired,
    sex: PropTypes.string,
    age: PropTypes.number
  }
  static defaultProps = {
    sex: "男",
    age: 18
  }
  render() {
    const { name, sex, age } = this.props
    return (
      <ul>
        <li>{name}</li>
        <li>{sex}</li>
        <li>{age + 1}</li>
      </ul>
    )
  }
}
const p = { name: "zhishouH" }
ReactDOM.render(<Person {...p} />, document.getElementById('app'))
```

完整代码：[组件实例属性——props](https://github.com/zhishouH/learn-react/tree/main/react-basic/07-%E7%BB%84%E4%BB%B6%E5%AE%9E%E4%BE%8B%E4%B8%89%E5%A4%A7%E5%B1%9E%E6%80%A7-props)

#### 7、组件实例属性——refs

```jsx
class Demo extends React.Component {
  showInput1 = () => {
  const { input1 } = this.refs
    alert(input1.value)
  }
  showInput2 = () => {
  const { input2 } = this
    alert(input2.value)
  }
  myRef = React.createRef()
  showInput3 = () => {
    alert(this.myRef.current.value)
  }
  render() {
    return (
      <div>
        {/*字符串形式*/}
        <input type="text" ref="input1" placeholder="input1" />
        <button onClick={this.showInput1}>点击弹出input1的值</button>
        {/*回调函数形式*/}
        <input type="text" ref={(current) => { this.input2 = current }} placeholder="input2" />
        <button onClick={this.showInput2} >点击弹出input2的值</button>
	    {/*createRef形式*/}
	    <input ref={this.myRef} type="text" placeholder="input3" /> 
	    <button onClick={this.showInput3}>点击弹出input3的值</button> 
      </div>
    )
  }
}
ReactDOM.render(<Demo />, document.getElementById('app'))
```

完整代码：[组件实例属性——refs](https://github.com/zhishouH/learn-react/tree/main/react-basic/08-%E7%BB%84%E4%BB%B6%E5%AE%9E%E4%BE%8B%E7%9A%84%E4%B8%89%E5%A4%A7%E5%B1%9E%E6%80%A7-refs)

#### 8、事件处理

```jsx
class Demo extends React.Component {
  // event.target
  // event.preventDefault() 阻止默认事件 
  handleClick = () => {
    alert("点击了")
  }
  render() {
    return (
      <button onClick={this.handleClick}>按钮</button>
    )
  }
}
ReactDOM.render(<Demo />, document.getElementById('app'))
```

- React 事件的命名采用小驼峰式（camelCase），而不是纯小写。
- 使用 JSX 语法时你需要传入一个函数作为事件处理函数，而不是一个字符串。

完整代码：[事件处理](https://github.com/zhishouH/learn-react/blob/main/react-basic/09-%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86/index.html)