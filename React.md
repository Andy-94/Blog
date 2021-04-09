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

##### refs

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

  Filter:

8.复习如何判断this的指向
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
