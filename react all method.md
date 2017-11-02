##跳转方式##

###1、【Component】.contextTypes###

****设置路由****

	//设置跳转路由router
	component.contextTypes = {
		router: prosType.any
	}
    //点击后跳转页面
     this.context.router.push({
       pathname: '/myMicroApp/authorityFail', //pathname代表地址
       state: 'string', //state是携带的参数
     })
****使用参数****

	console.log(this.props.location.state)  // string

###2、Route###

	import { Router, Route, hashHistory } from 'react-router';
	
	class App extends React.Component {
		render(){
			return(
				<Router history={ hashHistory }>
					<Route path='./user/:name' component={ Userpage }></Route>
				</Router>
			)
		}
	}
****指定参数****

****(1)Link组件实现跳转：****

	import {Link,hashHistory} from 'react-router';
	
	<Link to="/user/sam">用户</Link> // Link to 可接函数

	<Link to={openMicroApp}>用户</Link> // Link to 可接对象
	export const openMicroApp = {
	  pathname: '/help/openMicroApp',
	  query: { imgSrc: require('./openMicroApp.png'), title: '如何注册服务号&小程序'},
	};

****(2)history组件实现跳转：****
	
	import {Link,hashHistory} from 'react-router';
	
	hashHistory.push("/user/sam");

****使用参数****

	export default class UserPage extends React.Component{
	    constructor(props){
	        super(props);
	    }
	    render(){
	        return(<div>this.props.params.name</div>)
	    }
	}

****上面的方法可以传递一个或多个值，但是每个值的类型都是字符串，没法传递一个对象,如果传递的话可以将json对象转换为字符串，然后传递过去，传递过去之后再将json字符串转换为对象将数据取出来 
如：定义路由：****

	<Route path='/user/:data' component={UserPage}></Route>

****使用****

	var data = {id:3,name:sam,age:36};
	data = JSON.stringify(data);
	var path = `/user/${data}`;

	<Link to={path}>用户</Link>

	hashHistory.push(path);

###3、query###

****query方式使用很简单，类似于表单中的get方法，传递参数为明文： 
首先定义路由：****

	<Route path='/user' component={UserPage}></Route>	

	var data = {id:3,name:sam,age:36};
	var path = {
	  pathname:'/user',
	  query:data,
	}

	<Link to={path}>用户</Link>

	hashHistory.push(path);

****获取数据****

	var data = this.props.location.query;
	var {id,name,age} = data;

###4、state###

****state方式类似于post方式，使用方式和query类似， 
首先定义路由：****

	<Route path='/user' component={UserPage}></Route>
	
	var data = {id:3,name:sam,age:36};
	var path = {
	  pathname:'/user',
	  state:data,
	}

	<Link to={path}>用户</Link>

	hashHistory.push(path);

****获取数据：****

	var data = this.props.location.state;
	var {id,name,age} = data;
	
