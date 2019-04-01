### ES6-对象以及对象的扩展

@(ES6)[ES6]

- 对象的属性简写

```
const foo = 'bar';
const baz = {foo};
baz // {foo: "bar"}

// 等同于
const baz = {foo: foo};
```
- 对象的方法简写

```javascript
const o = {
  method() {
    return "Hello!";
  }
};

// 等同于
const o = {
  method: function() {
    return "Hello!";
  }
};
```
- CommonJS模块输出一组变量，就非常适合简写
```
let ms = {};
function getItem (key) {
  return key in ms ? ms[key] : null;
}
function setItem (key, value) {
  ms[key] = value;
}
function clear () {
  ms = {};
}

module.exports = { getItem, setItem, clear };
// 等同于
module.exports = {
  getItem: getItem,
  setItem: setItem,
  clear: clear
};
```
- 对象方法的name属性，返回函数名
```
const person = {
  sayName() {
    console.log('hello!');
  },
};
person.sayName.name   // "sayName"
```
> 属性的遍历
ES6 一共有 5 种方法可以遍历对象的属性。

（1）for...in

for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

（2）Object.keys(obj)

Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

（3）Object.getOwnPropertyNames(obj)

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

（4）Object.getOwnPropertySymbols(obj)

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性的键名。

（5）Reflect.ownKeys(obj)

Reflect.ownKeys返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

以上的 5 种方法遍历对象的键名，都遵守同样的属性遍历的次序规则。
- 对象的解构赋值
- 对象的扩展运算符

##### 对象的新增方法
- Object.is():用来比较两个值是否严格相等
```
Object.is('foo', 'foo')// true
Object.is({}, {})// false
Object.is(NaN, NaN) // true
```
- Object.assign(target,...source):用于对象的合并，将源对象（source）的所有**可枚举属性**，复制到目标对象（target）。
```
const target = { a: 1 };
const source1 = { b: 2 };
const source2 = { c: 3 };
//第一个参数是目标对象，后面所有的参数都是源对象
Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```
Object.assign常见用途
（1）为对象添加属性
```
class Point {
  constructor(x, y) {
    Object.assign(this, {x, y});
  }
}
```
（2）为对象添加方法
```
Object.assign(SomeClass.prototype, {
  someMethod(arg1, arg2) {
    ···
  },
  anotherMethod() {
    ···
  }
});

// 等同于下面的写法
SomeClass.prototype.someMethod = function (arg1, arg2) {
  ···
};
SomeClass.prototype.anotherMethod = function () {
  ···
};
```
(3)克隆对象:只能克隆原始对象自身的值
```
function clone(origin) {
  return Object.assign({}, origin);
}
```
(4)合并多个对象
```javascript
//将多个对象合并到某个对象。
const merge =
  (target, ...sources) => Object.assign(target, ...sources);
  
//如果希望合并后返回一个新对象，可以改写上面函数，对一个空对象合并。
const merge =
  (...sources) => Object.assign({}, ...sources);
```
（5）为属性指定默认值
