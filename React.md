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

19.路由 route
	组成: key—虚拟路径。    Value —组件
	特点: 浏览器地址栏输入网址，浏览器不会发出请求
	
	需要下载  yarn add react-router-dom
	现需要在index.js中添加<BrowserRouter>
	a标签改为 <Link. … to=“/xxx”/> home</Link > or <NavLink></NavLink> —高亮
	如果需要调整颜色：需要加入: activeClassName=“xxx”
	多个pages路由需要Switch
	检测地址的变化 <Switch><Route path=“/xxx” component={home}/><Switch>
	自动切换当前路由页面<Redirect to=“”> 
	需要引入的有 import {NavLink,Route,Switch,Redirect} from ‘react-router-dom

路由默认是模糊匹配 加入exact={true}后会变成精准匹配
在Link中添加replace 将会取消后退历史
调用函数 this.props.history.push	() 添加历史记录 (需要用到()=>{this.function()})进行传参
前进: this.props.history.goForward
后退: this.props.history.goBack

如果要变成一个路由组件使用 withRouter
	export default withRouter(Nav)

路由组件会在props中多出

	1.history —location, replace, goBack, goForward
	2.location —pathname
	3.match — params

当路由需要传参数时:
	<Link to={`/home/message/${id}`}>
	<Route to=‘/home/message/:id”>占位符
然后 通过: const {id} =. This.props.match.params 确定id
便利id: const result= this.state.detail.find((details)=>{return detail.id === id})

20.组件
一般组件—component   程序员标签渲染的组件
路由组件—pages	   react-router帮渲染的
(用componentDidUnmount检测路由是否是隐藏或者卸载，其实是卸载)
BrowserRouter 改成HashRouter 能解决路径样式问题
%PUBLIC_URL% 能解决路径样式问题

21.刷新时，路由会出现问题（默认选中但是刷新无用）

	引入 withRouter
	Import {withRouter} from  'react-router-dom'
	export default withRouter(Nav)
	调用:
	    const selectedKeys = this.props.location.pathname.split("/")
	    const selectedOpenkey = selectedKeys.reverse()[0] //最后一个key

22. ant的坑
defaultSelectedKeys 只能引入一个，然后选取一个，在登陆时会出现问题，解决方案，使用selectedKeys 能引入多个.
rowKey 可以改变数据库rowKey = '_id'

pagination 分页器


23.状态码
	200 - 请求成功
	301 - 资源（网页等）被永久转移到其它URL
	404 - 请求的资源（网页等）不存在
	500 - 内部服务器错误
	1**	信息，服务器收到请求，需要请求者继续执行操作
	2**	成功，操作被成功接收并处理
	3**	重定向，需要进一步的操作以完成请求
	4**	客户端错误，请求包含语法错误或无法完成请求
	5**	服务器错误，服务器在处理请求的过程中发生了错误

25. token模式
输入username/password 校验成功 生成token
请求api时用token，通过过滤器校正token，如果通过返回请求数据
如果没通过返回错误码401

token会保持在session中


25.//路由跳转时，nav会高亮
    if(selectedKeys.indexOf('product') !== -1) selectedOpenkey ='product'

26.
Nprogress 进度条库
	yarn add nprogress
然后引入自身css
import 'nprogress/nprogress.css'
在axios中 
在request 中加入NProgress.start();
esponse 中加入NProgress.done();

27
在react中需要识别标签数据时
需要用<span dangerouslySetInnerHTML={{__html:detail}}></span>

28 
当用到Form组件时如果需要用到button提交时需要用到
<Button htmlType="submit"  type="primary">Submit</Button>


29.
文本编辑器库.  wysiwyg

30.
实现数据没法第一时间读取到，不能用state方法时，用ref + this.myRefForm.current.setFieldsValue(data)
getIdData = async(id)=>{
    let result = await reqCategoryDetail(id)
    const {status,data,msg} = result
    if(status ===0){
      //andt直接引入data的数据，只要原本form的数据和数据库的数据一致
      this.myRefForm.current.setFieldsValue(data)
    }else{
      message.error(msg)
    }

31.
有时候从state中获取对象类型数据的时候，最好断开引用
比如:
Let {a}= this.state
改成
Let a = […this.state.a]

32. 数组中some方法 (返回值为boole)
34. 
 //验证用户权限
  RoleAuth =(menuObj)=>{
    const {rolePin} = this.props
    if(this.props.userName ==='admin') return true
    if(!menuObj.children){
      return rolePin.find((item)=> item === menuObj.key)
    }else{
      return menuObj.children.some((item2)=>rolePin.indexOf(item2.key) !== -1 )
    }
  }

34.数据可视化
ECharts
安装react版本和echarts
yarn add echarts-for-react echarts


35.pureComponent和component区别
Component问题：
1.父组件重新render(),子组件也会重新执行render()，即使没有任何变化
2.当前组件setState({}) 子组件也会重新执行render()
解决问题:
PurceComponent代替Compoent
PureComponent比Component智能很多

组件哪个生命钩子能实现组件优化?
shouldCompoentUpdate().

36。新特性
1. State Hook: React.useState()

2. Effect Hook: React.useEffect()
是一个三个生命周期组合
3. Ref Hook: React.useRef()
用法和React.CreateRef差不多











