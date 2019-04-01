react-redux和redux的使用
===
@(React)
//安装redux
```
npm install redux
```
//安装react-redux
```
npm install react-redux
```
##### 项目目录结构
* src
	+ store
		- index.js
	+ reducers
		- index.js
###### 使用redux
```javascript
//store	index.js
import {createStore} from 'redux';
import reducers from `../reducers/index.js` 
//创建状态仓库
const store = createStore(reducers);
export default store;
```
```javascript
//reducer index.js
const defaultState = {};
export default(state = defaultState,action)=>{
	return state;
}
```
##### 使用react-redux
```javascript
//在根文件index.js中
import {Provider} from 'react-redux';
...
//Provider提供了一个空间,存储的redux中所有的状态,然后使用react-redux中的connect方法,能够直接连接到这个空间,去操作里面的数据
<Provider store={store}><App /></Provider>

//让Header组件连接到store,在Header组件里index.js
import {connect} from 'react-redux';
...
const mapStateToProps = (state)=>{
	return {
		//数据
		focused:state.focused}
}
const mapDispathToProps=(dispath)=>{
	return {rops,mapDispathToProps
		//操作数据的方法
	}
}
export default connect(mapStateProps,mapDispathToProps)(Header)
```

- Action
就是View发出的通知，表示State应该要发生变化了。
Action 是一个对象。其中的type属性是必须的，表示 Action 的名称。

```
const action = {
  type: 'ADD_TODO',
  payload: 'Learn Redux'//就是传过去的数据
};
```
- Reducer（对state进行操作）
Reducer是一个函数，store接受到action和当前state作为参数，返回一个新的state。
```
const reducer = function (state, action) {
  // ...
  return new_state;
};
```
store.dispatch方法会触发 Reducer 的自动执行。为此，Store 需要知道 Reducer 函数，做法就是在生成 Store 的时候，将 Reducer 传入createStore方法。
```javascript
import { createStore } from 'redux';
const store = createStore(reducer);
```
> 注意：Reducer 函数里面不能改变 State，必须返回一个全新的对象

```javascript
// State 是一个对象
function reducer(state, action) {
  return Object.assign({}, state, { thingToChange });
  // 或者
  return { ...state, ...newState };
}

// State 是一个数组
function reducer(state, action) {
  return [...state, newItem];
}
```
##### Store的三个方法
- store.getState()
- store.dispatch()
- store.subscribe()
```
//只要把 View 的更新函数（对于 React 项目，就是组件的render方法或setState方法）放入listen，就会实现 View 的自动渲染。

let unsubscribe = store.subscribe(() =>
  let newState = store.getState();
  component.setState(newState);
);
//store.subscribe方法返回一个函数，调用这个函数就可以解除监听。
unsubscribe(); //解除监听
```
###  redux

  
  深入理解redux中的state与react的state的区别
- redux的state存放的是全局的长期数据,类似数据库的功能
- React组件内部的state存放的是临时内部状态数据(**例如窗口的打开或关闭**),所以这两个state没有任何关系

---
- 组件的state的使用场景
1. 保持UI的状态
2. 存储暂时的数据(例如表单的输入)

- Redux 的state的应用场景
1. 保持除UI状态外的应用状态(例如用户的登录状态),当登录状态改变时,有多个组件需要访问这个数据信息作出响应,这些组件(至少有一个)需要重新渲染与更新数据.

---
从组件角度看，如果你的应用有以下场景，可以考虑使用 Redux。
- 某个组件的状态，需要共享
- 某个状态需要在任何地方都可以拿到
- 一个组件需要改变全局状态
- 一个组件需要改变另一个组件的状态