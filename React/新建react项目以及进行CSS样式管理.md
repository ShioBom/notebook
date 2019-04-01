#### 新建react项目以及进行CSS样式管理

@(React)

* 安装react环境(只安装一次)
```
npm install -g create-react-app myapp
```
* 创建react项目(myapp)
```
create-react-app myapp
//启动
cd myapp
npm start
```
* 安装管理css样式的模块 Styled-Components(vscode已支持智能提示)
```
npm install --save styled-components
```
1. 使用方法
1.1 将原本的css文件改变成style.js文件
```javascript
//全局样式
import {injectGlobal} from `styled-components`;
injectGlobal`
	body{
		margin:0;
		padding:0;
		font-family:sans-serif;
		background:green
	}
`

//局部样式
import styled from `styled-components`;
import logoPic from `../../statics/logo.png`
//这里创建的组件首字母必须大写
export const HeaderWrapper = styled.div`
	heignt:56px;
	background:red;
`
export const Logo = styled.a.attrs({
	href:"/"
})`
	background:url(${logoPic})
`
//组件内部导入
import {HeaderWrapper} from `./style.js`
//组件内部使用
class Header extends Component{
	render(){
		return (
			//这样就创建了一个带样式的div标签
			<HeaderWrapper>header</HeaderWrapper>
		)
	}
}
```
```javascript
//一些技巧,style.js
export const NavItem = styled.div`
	&.left{
		float:left;
	}
	&.right{
		float:right;
	}
	&.active{
		color:red;
	}
`
//index.js
<NavItem className="left"></NavItem>
<NavItem className="active"></NavItem>
<NavItem className="right"></NavItem>
```
* reset.css,将样式重置放到全局样式里
##### 在react项目中使用scss
安装组件node-sass ,sass-loader
```
npm install node-sass sass-loader
```
##### 在react中使用swiper插件
```
npm install swiper
//这里的引入是为了后期打包不报错
import Swiper from 'swiper/dist/js/swiper.js'
import 'Swiper/dist/css/swiper.min.css'
```
##### 将组件写成无状态组件
- 就是没有组件内部state的组件
- 优点:性能会比较高
```
import {HeaderWrapper} from `./style.js`
const Header = (props)=>{
	return(
		<HeaderWrapper>header</HeaderWrapper>
	)
}
```
 
