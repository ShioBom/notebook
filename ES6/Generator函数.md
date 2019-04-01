### Generator函数

@(ES6)

可以理解为generator函数是一个**状态机**，封装了多个内部状态，执行generator函数会返回一个遍历器对象，所以该函数也是一个**遍历器对象生成函数**。
- Generator函数与普通函数的区别
	- 一是，function关键字与函数名之间有一个星号
	- 二是，函数体内部使用yield表达式，定义不同的内部状态
```javascript
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}
//该函数有三个状态：hello，world，return语句
var vw= helloWorldGenerator();
//该函数这时并不会执行，返回一个指向内部状态的指针对象。
  console.log(vw.next());
  //这个函数执行了！！！{value: "hello", done: false}
  console.log(vw.next()); 
  //{value: "world", done: false}
  console.log(vw.next()); 
  //{value: "ending", done: true}
  console.log(vw.next());
  //{value: undefined, done: true}

//done的值为false，表示遍历还没有结束，当执行到return语句或函数执行完done的值会变为true。
```
> 可以看出，Generator函数是分段执行的，yield表达式是暂停执行的标记，而next方法可以恢复执行，直至遇到下一个yield。紧跟在yield后面的那个表达式的值，作为返回的对象的value属性值。

- yield表达式如果用在另一个表达式中，必须用小圆括号括起来
```java
function* demo() {
  console.log('Hello' + yield); 
  // SyntaxError
  console.log('Hello' + yield 123); 
  // SyntaxError
  console.log('Hello' + (yield)); // OK
  console.log('Hello' + (yield 123)); // OK
}
```
- yield表达式用作函数参数或放在赋值表达式的右边，可以不加括号。
```javascript
function* demo() {
  foo(yield 'a', yield 'b'); // OK
  let input = yield; // OK
}
```
> 由于next方法的参数表示上一个yield表达式的返回值，所以在第一次使用next方法时，传递参数是无效的。
```javascript
function* foo(x) {
  var y = 2 * (yield (x + 1));
  var z = yield (y / 3);
  return (x + y + z);
}

var a = foo(5);
a.next() // Object{value:6, done:false}
a.next() // Object{value:NaN, done:false}
a.next() // Object{value:NaN, done:true}

var b = foo(5);
b.next() // { value:6, done:false }
b.next(12) // { value:8, done:false }
b.next(13) // { value:42, done:true }

//上面代码第一次调用b的next方法时，返回x+1的值6；第二次调用next方法，将上一次yield表达式的值设为12，因此y等于24，返回y / 3的值8；第三次调用next方法，将上一次yield表达式的值设为13，因此z等于13，这时x等于5，y等于24，所以return语句的值等于42。
```
Generator对象用途
- 给原生对象加上iterator接口
```javascript
//方式一
function* objectEntries(obj) {
  let propKeys = Reflect.ownKeys(obj);

  for (let propKey of propKeys) {
    yield [propKey, obj[propKey]];
  }
}

let jane = { first: 'Jane', last: 'Doe' };

for (let [key, value] of objectEntries(jane)) {
  console.log(`${key}: ${value}`);
}
// first: Jane
// last: Doe

//方式二:将 Generator 函数加到对象的Symbol.iterator属性上面。
function* objectEntries() {
  let propKeys = Object.keys(this);

  for (let propKey of propKeys) {
    yield [propKey, this[propKey]];
  }
}

let jane = { first: 'Jane', last: 'Doe' };

jane[Symbol.iterator] = objectEntries;

for (let [key, value] of jane) {
  console.log(`${key}: ${value}`);
}
// first: Jane
// last: Doe
```
除了for...of循环以外，扩展运算符（...）、解构赋值和Array.from方法内部调用的，都是遍历器接口。这意味着，它们都可以将 Generator 函数返回的 Iterator 对象，作为参数。
```javascript
function* numbers () {
  yield 1
  yield 2
  return 3
  yield 4
}

// 扩展运算符
[...numbers()] // [1, 2]

// Array.from 方法
Array.from(numbers()) // [1, 2]

// 解构赋值
let [x, y] = numbers();
x // 1
y // 2

// for...of 循环
for (let n of numbers()) {
  console.log(n)
}
// 1
// 2
```