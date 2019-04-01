### ES6- Set

@(ES6)

- 它类似于数组，但是成员的值都是==唯一==的，没有重复的值,Set本身是一个==构造函数==，用来生成 Set 数据结构。
- Set函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化。
```js
// 去除数组的重复成员
const set = new Set([1, 2, 3, 4, 4]);
[...set]
// [1, 2, 3, 4]
```
- 向 Set 加入值的时候，不会发生类型转换，所以5和"5"是两个不同的值。
- 两个对象总是不相等的。
```js
let set = new Set();

set.add({});
set.size // 1

set.add({});
set.size // 2
```
##### 操作方法
- add(value)：添加某个值，返回 Set 结构本身。
- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
- has(value)：返回一个布尔值，表示该值是否为Set的成员。
- clear()：清除所有成员，没有返回值。
##### 遍历方法
- keys()：返回键名的遍历器
- values()：返回键值的遍历器
- entries()：返回键值对的遍历器
- forEach()：使用回调函数遍历每个成员
```js
let set = new Set(['red', 'green', 'blue']);

for (let item of set.keys()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.values()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.entries()) {
  console.log(item);
}
// ["red", "red"]
// ["green", "green"]
// ["blue", "blue"]
```
## Map
1. ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。
2. 任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构（详见《Iterator》一章）都可以当作Map构造函数的参数。这就是说，Set和Map都可以用来生成新的 Map。
>注意，只有对同一个对象的引用，Map 结构才将其视为同一个键。
```js
const map = new Map();

map.set(['a'], 555);
map.get(['a']) // undefined
```
##### 属性
- size属性:size属性返回 Map 结构的成员总数。
- set(key, value):set方法设置键名key对应的键值为value，然后返回整个 Map 结构。如果key已经有值，则键值会被更新，否则就新生成该键。
- get(key):get方法读取key对应的键值，如果找不到key，返回undefined。
- has(key):has方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。
- delete(key):delete方法删除某个键，返回true。如果删除失败，返回false。
- clear():清空map,没有返回值
##### 遍历方法
- keys()：返回键名的遍历器。
- values()：返回键值的遍历器。
- entries()：返回所有成员的遍历器。
- forEach()：遍历 Map 的所有成员。
```js
const map = new Map([
  ['F', 'no'],
  ['T',  'yes'],
]);

for (let key of map.keys()) {
  console.log(key);
}
// "F"
// "T"

for (let value of map.values()) {
  console.log(value);
}
// "no"
// "yes"

for (let item of map.entries()) {
  console.log(item[0], item[1]);
}
// "F" "no"
// "T" "yes"

// 或者
for (let [key, value] of map.entries()) {
  console.log(key, value);
}
// "F" "no"
// "T" "yes"

// 等同于使用map.entries()
for (let [key, value] of map) {
  console.log(key, value);
}
// "F" "no"
// "T" "yes"
```