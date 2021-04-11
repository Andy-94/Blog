# App/

      import React,{Component} from 'react'
      import './App.less'

      export default class App extends Component{
        state = {
          repoName:'',
          repoUrl:'',
          loading:'',
          errorMessage:''
        }
        async componentDidMount(){
          const URL = ''
          try{
            let response = await axios.get(URL)
            let data = response.data.item[0]
            this.setState({
              repoName:data.name,
              repoUrl:data.html_url,
              loading:false,
              errorMessage:''
            })
          }catch(err){
            this.setState({
              repoName:'',
              repoUrl:'',
              loading:false,
              errorMessage:err.message
            })
          }
        }
        render(){
          let {repoName,repoUrl,loading,errorMessage} = this.state
          if(loading){
            return <h2>Loading...</h2>
          }else if(repoName && repoUrl){
            return <h2>github:<a href={repoUrl}>{repoName}</a></h2>
          }else if(errorMessage){
            return <h2 style={{color:'red'}}>{errorMessage}</h2>
          }
        }
      }
