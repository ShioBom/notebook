### ES6-数组的扩展

@(ES6)

#### 扩展运算符(...)
相当于是rest参数的逆运算,将一个数组转为用逗号分隔的参数序列。
> 该运算符主要用于函数调用。

```
console.log(...[1, 2, 3])
// 1 2 3
console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

```

##### 扩展运算符的应用:
- 替代函数的 apply 方法

```js
// ES5 的写法
Math.max.apply(null, [14, 3, 77])
// ES6 的写法
Math.max(...[14, 3, 77])
// 等同于
Math.max(14, 3, 77);

// ES5的 写法
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
Array.prototype.push.apply(arr1, arr2);
// ES6 的写法
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];
arr1.push(...arr2);
```
- 复制数组(深拷贝)
 > 修改原数组的值,会反映到新数组
```js
const a1 = [1, 2];
// 写法一
const a2 = [...a1];
// 写法二
const [...a2] = a1;
```
- 合并数组
> 修改原数组的值,会反映到新数组
```
const arr1 = ['a', 'b'];
const arr2 = ['c'];
const arr3 = ['d', 'e'];
// ES5 的合并数组
arr1.concat(arr2, arr3);
// [ 'a', 'b', 'c', 'd', 'e' ]
// ES6 的合并数组
[...arr1, ...arr2, ...arr3]
// [ 'a', 'b', 'c', 'd', 'e' ]
```
- 与解构赋值结合

```
// ES5
a = list[0], rest = list.slice(1)
// ES6
[a, ...rest] = list
```
- 字符串
- 具有iterater接口的
- Map,Set,Generator函数
##### Array.from()
> Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）
- 类数组(所谓类似数组的对象，本质特征只有一点，即必须有length属性。)
```
//常见的类似数组的对象是 DOM 操作返回的 NodeList 集合，
//以及函数内部的arguments对象。Array.from都可以将它们转为真正的数组。
// NodeList对象
let ps = document.querySelectorAll('p');
Array.from(ps).filter(p => {
  return p.textContent.length > 100;
});
// arguments对象
function foo() {
  var args = Array.from(arguments);
  // ...
}
```
- 可遍历的对象
```js
Array.from('hello')
// ['h', 'e', 'l', 'l', 'o']

let namesSet = new Set(['a', 'b'])
Array.from(namesSet) // ['a', 'b']
```
> Array.from还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。
```js
Array.from(arrayLike, x => x * x);
// 等同于
Array.from(arrayLike).map(x => x * x);
Array.from([1, 2, 3], (x) => x * x)
// [1, 4, 9]

Array.from({ length: 2 }, () => 'jack')
// ['jack', 'jack']
```
##### Array.of()
> Array.of方法用于将一组值，转换为数组。
##### copeWithin()
> 数组实例的copyWithin方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。

- target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
- start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示倒数。
 - end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。

```
//三个参数都应该是数值,
[1, 2, 3, 4, 5].copyWithin(0, 3)
// [4, 5, 3, 4, 5]
```
##### find() 
> 数组实例的find方法，用于找出第一个符合条件的数组成员。如果没有符合条件的成员，则返回==undefined==,参数是==回调函数==
##### findIndex()
> 返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则==返回-1==。参数是==回调函数==
##### fill()
> fill方法使用给定值，填充一个数组。
##### entries()，keys() 和 values()
> 用于遍历数组。它们都返回一个遍历器对象，可以用for...of循环进行遍历，唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。
```js
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```
##### 数组实例的 includes()
> 返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。(2016年,会有兼容问题),该方法的第二个参数表示搜索的起始位置，默认为0。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为-4，但数组长度为3），则会重置为从0开始。
```
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
```
##### 数组实例的 flat()，flatMap()
##### 数组对空位的处理不一,所以应避免出现空位