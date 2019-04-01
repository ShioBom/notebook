### ES6-函数的扩展

@(ES6)


##### 参数默认值
- ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面。
> 使用参数默认值时，函数不能有同名参数。
```js
// 不报错
function foo(x, x, y) {
  // ...
}
// 报错
function foo(x, x, y = 1) {
  // ...
}
// SyntaxError: Duplicate parameter name not allowed in this context
```
- 只有当函数foo的参数是一个对象时，变量x和y才会通过解构赋值生成。如果函数foo调用时没提供参数，变量x和y就不会生成，从而报错
```
function foo({x, y = 5}) {
  console.log(x, y);
}
foo({}) ;// undefined 5
foo({x: 1, y: 2}); // 1 2
foo() ;//TypeError: Cannot read property 'x' of undefined

//通过提供函数参数的默认值，就可以避免这种情况。
function foo({x, y = 5} = {}) {
  console.log(x, y);
}
foo() // undefined 5
```
###### 一个例子
> 区别是写法一函数参数的默认值是空对象，但是设置了对象解构赋值的默认值；写法二函数参数的默认值是一个有具体属性的对象，但是没有设置对象解构赋值的默认值。
```
// 写法一
function m1({x = 0, y = 0} = {}) {
  return [x, y];
}
// 写法二
function m2({x, y} = { x: 0, y: 0 }) {
  return [x, y];
}
// 函数没有参数的情况
m1(); // [0, 0]
m2(); // [0, 0]

// x 和 y 都有值的情况
m1({x: 3, y: 8}); // [3, 8]
m2({x: 3, y: 8}); // [3, 8]

// x 有值，y 无值的情况
m1({x: 3}); // [3, 0]
m2({x: 3}); // [3, undefined]

// x 和 y 都无值的情况
m1({}); // [0, 0];
m2({}); // [undefined, undefined]

m1({z: 3}); // [0, 0]
m2({z: 3}); // [undefined, undefined]
```
##### 参数默认值的位置
通常情况下，定义了默认值的参数，应该是函数的尾参数。==如果非尾部的参数设置默认值，实际上这个参数是没法省略的。==

```js
function f(x = 1, y) {
  return [x, y];
}

f() // [1, undefined]
f(2) // [2, undefined])
f(, 1) // 报错
```
##### 函数的length属性
1. length属性的含义是，该函数预期传入的参数个数
2. 指定了默认值以后，函数的length属性，将返回没有指定默认值的参数个数
3. 如果设置了默认值的参数不是尾参数，那么length属性也不再计入后面的参数了
4. 函数的length属性，不包括 rest 参数。
##### 函数name属性
函数的name属性，返回该函数的函数名。
```
function foo() {}
foo.name // "foo"
```
##### rest参数
ES6 引入 rest 参数（形式为...变量名），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。
> 注意，rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。

> 函数的 length 属性，不包括rest参数

###### 与arguments的区别
- rest参数只包括那些没有给出名称的参数，arguments包含所有参数
- arguments 对象不是真正的数组，而rest 参数是数组实例，可以直接应用sort, map, forEach, pop等方法
- arguments 对象拥有一些自己额外的功能
##### 箭头函数
作用:1.简化回调函数
###### 注意点
箭头函数有几个使用注意点。

（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。

（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。
###### 不适用的场合
第一个场合是定义函数的方法，且该方法内部包括this。
```js
const cat = {
  lives: 9,
  jumps: () => {
    this.lives--;
  }
}
```
第二个场合是需要动态this的时候，也不应使用箭头函数。
```js
var button = document.getElementById('press');
button.addEventListener('click', () => {
  this.classList.toggle('on');
});
```


