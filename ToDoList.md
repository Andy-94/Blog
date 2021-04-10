App/

    export default class App extends Component{
      state={
        list:['reading book','playing game','listening music']
      }
      addList =(data)=>{
        let {list} = this.state
        list.unshift(data)
        this.setState({list})
      }

      render(){
        return (
          <div className="app">
            <h1>This is TodoList Case</h1>
            <TodoInput count={this.state.list.length} addList={this.addList}/>
            <Todolist list={this.state.list}/>
          </div>
        )
      }
    }
    
 /TodoInput
 
     export default class TodoInput extends Component{
      myRef = React.createRef()
      add =()=>{
        let {value} = this.myRef.current
        let data = value
        if(!data) return 
        let {addList} = this.props
        addList(data)
        this.myRef.current.value=''
      }
      render(){
        let {count} = this.props
        return (
          <div>
            <input type="text" ref={this.myRef}/>
            <button onClick={this.add}>List#{count}</button>
          </div>
        )
      }
    }
 
 
 /TodoList
 
     export default class Todolist extends Component{
      static propTypes = {
        list:PropTypes.array.isRequired
      }
      render(){
        let {list} = this.props
        return (
          <ul>
            {list.map((item,index)=>{return <li key={index}>{item}</li>})}
          </ul>
        )
      }
    }
 
