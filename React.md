# React notice
1.React的概念理解：
	声明式declarative、组件化coponent-based、虚拟DOM(virtualDOM)
	VDOM就是js中的object对象，比较轻，没有太多属性。
2.jsx语法规范:
  
    1.标签闭合
    2.style={{color:’red’}}
    3.class 为 className
    4.不是js中的字符串，不允许加单引号
    5.标签中写js表达式必须加{}
      用jsx： 
        VDM= ‘<h1>helloworld</h1>)’
        ReactDOM.render(VDM, document.getElementById(‘’))
      用js：React.createElement('h1',  {id:'myTitle'},  title)
      jsx使用style标签时：
        return (<h1><span style={{colour:’red’}}>hello</span></h1>)

3.React基本编码流程.
    第一步，定义组件
    第二步，render()渲染标签

    export default class App extends React.Component{
      render(){
        return (<div></div>)
      }
    }
    ReactDOM.render(</App>,document.getElementById(‘’))

4.定义组件的两种方式
    模块：向外提供特定功能的js程序，一般就是一个js文件
    组件：用来实现特定界面功能效果的代码和资源的集合

5.组件三大属性

##### state案例
    初始化状态：
    constructor(…props){ 	super(…props)
      this.state = {
        stateProp1:value1,
        stateProp2:value2,
      }
    }
    读取状态
    this.state.statePropertyName
    更新
    this.setState({
        stateProp3:value1,
        stateProp4:value2,
    })
##### props
    内部读取：
      this.props.xxx
    使用prop-types库进行限制 (往类自身添加属性用 static)
    static propTypes ={
      name: PropTypes.string.isRequired,
      age:PropTypes.number
    }
    默认属性:
    static defaultProps = {age:18, sex:’man’}
    扩展属性：
    <Person {…person}/>

##### ref
####老版本API:
	在不是自己的input中调用，需要用到refs字符串形式
		<input type=“” ref=“input1”
		<button onClick ={this.handleClick}
	然后根据
		let input1 =. This.refs.input1 获取此节点
	在自己的input中不需要调用refs
		<input onClick ={this.inputClick}
	然后根据event寻找此节点
		inputClick = (event) =>{alert(event.target.value)}
####新版本1
Refs回调函数直接透过箭头函数回调当前节点。
	<input type=“text” ref={(current)=>{this.input1 = current}}>
精简:	<input type=“text” ref={(current)=>this.input1 = current}>
	然后
	alert(this.input1.value)
####新版本2
Refs 容器，创建一个容器，此容器包含整个节点
	myRef = React.createRef()
	<input type=“text” ref={this.myRef}>
	然后
	alert(this.myRef.current.value)

6.三点运算符
   浅克隆
    Let data = {name:”andy”, age:”12”,gender:”male”…}
    <Person {…data}/>
    let data2 = {…data}
    data2 ===data  不等
7.数组上的map、forEach、find、filter方法怎么用？都有什么特点？
  Map:
    let arr={’Andy’, ’Kimi’}
    {arr.map((item, index)=><li key={index}>{item}</li>)}
  forEach:

  Find:
  	
	const {id} = this.props.match.params
	const result = this.state.detail.find((details)=>{return detail.id === id})
  Filter:
  	
	const {id} = this.props
	const result = id.filter((detail)=>{return detail.id === id})

8.如何判断this的指向
	jsx中编译后的js为严格模式，所以this is undefined.
	可以在constructor中遍历引入函数blind（this)
	箭头函数 ()=>{}
9.复习bind、apply、call怎么用？有什么区别？

10.bind的返回值是什么？
	当函数调用bind时候，直接在原本函数上添加值：在constructor里面用blind(this)将负值整个class中的全局变量
  This.change.blind(this)
 
11.深度克隆手写一遍

      function deepClone(obj) {
          let newObj = Array.isArray(obj) ? [] : {}
          if (obj && typeof obj === "object") {
              for (let key in obj) {
                  if (obj.hasOwnProperty(key)) {
                      newObj[key] = (obj && typeof obj[key] === 'object') ? deepClone(obj[key]) : obj[key];
                  }
              }
          } 
          return newObj
      }
      const newObj = deepClone(oldObj));
12.受控组件


	import React,{ Component} from 'react'
	export default class Control extends Component{
	  state={username:''}
	  myRef = React.createRef()
	  handleOnclick=(event)=>{
	    let {value} = this.myRef.current
	    event.preventDefault();
	    console.log(`this username is ${this.state.username} and the password is ${value}`)
	  }
	  handleUsername =(event)=>{
	    let {value} = event.target
	    this.setState({username:value})
	  }
	  render(){
	    return(
	      <form onClick={this.handleOnclick} action="http://www.baidu.com">
		<input type="username" onChange={this.handleUsername}/>
		<button>this is button</button>
		<input type="password" ref={this.myRef}/>
	      </form>
	    )
	  }
	}
13. React的生命周期
	render 每次都自动调用
最重要的：
	componentDidMount. 挂载 （组件一旦挂载完成，componentDIdMount 只会调用一次
	componentWillUnmount() 卸载的前一刻 将被调用
流程：

	initial render -> constructor() -> componentWillMount() -> render() -> componentDIdMount -> componentWillUnmount()

	componentWillUpdate() 和componentDidUpdate() 每次render中有改变时更新

	shouldComponentUpdate()是控制this.setState()的开关，只有true和false

初始化： constructor(), componentWillMount(), render(), componentDidMount()
更新: shouldComponentUpdate(), componentWillUpdate(), render(), componentDidUpdate()
卸载: componentWillUnmount()
新引进: getDerivedStateFromProps(props, state) 必须添加return 返回一个props 或者state更新，可以和componentDidUpdate()一起用

14.diff算法
在虚拟dom中，修改时，对比修改前的dom tree。只修改当前改变的部分内容。只对一个节点进行重回重排

15.遍历map方法中， key不能用index代替，因为在react的虚拟dom内部中旧的key会对比当前的key。但是对比后会发现相同的会保留数据。
解决办法用唯一标识作为key，可以直接在state中写入id作为唯一标识 

16.询问是否删除（必须要有window)
	
	window.confirm(‘do you need detel’)
17.技巧

	onClick(()=>{this.detel()}) 带入函数
18. React ajax. fetch  组件通讯方式

		1. Props通讯， 1.父传子 (实用)  2. 祖先传子。 但是比较麻烦
		2. 使用消息订阅技术 1.任意组件通讯 subscribe（订阅） 和 publish （发布）
		    1. 需要使用PubSub.js. npm install pubsub-js
		    2. 引入 import PubSub from ‘pubsub-js’
		    3. 先订阅 需要放在componentDidMount里面 PubSub.subscribe('MY TOPIC', （msg.data）=>{});
		    4. 发布PubSub.publish('MY TOPIC', 'hello world!');

		1. redux








