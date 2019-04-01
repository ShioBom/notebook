### ES6-let 和const

@(ES6)

##### let
- let用来声明变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效。

```javascript
{
    let b = 2;
    var a = 1;
}
console.log(a);
console.log(b);// b is not defined
```
for循环的计数器，就很合适使用let命令

```javascript
for(var i=0;i<5;i++){
    //yourcode
}
console.log("i="+i);//i=5,i在循环体内外都有效
for(let j=0;j<5;j++){
    //your code
}
console.log("j="+j);//ReferenceError: j is not defined,计数器j只在for循环体内有效
```
```
// eg.3
var a = [];
for( var i = 0; i < 5; i++ ) {
    a[i] = function() {
        console.log( "i = " + i );
    }
}
a[3]();
// output: i = 5

let b = [];
for( let j = 0; j < 5; j++ ) {
    b[j] = function() {
        console.log( "j = " + j );
    }
}
b[3]();
// output: j = 3
```
- 变量i是var声明的，在全局范围内都有效。所以每一次循环，新的i值都会覆盖旧值，导致最后输出的是最后一轮的i的值。
- 变量i是let声明的，当前的i只在本轮循环有效，所以每一次循环的i其实都是一个新的变量
> let和const都不存在变量提升
##### const
1. const声明一个只读的==常量索引==。一旦声明，该索引就不能改变。值是可以改变的(string和number除外)

```JavaScript
const names = [ ] ;
names . push ( “Jordan” ) ;
console . log ( names ) ;//Jordan
names = ['Jordan'];
console.log(names);//会报错
```


    const YY = "37";
    console.log( YY );
    
    YY = "67";
    console.log( YY );
    // TypeError: Assignment to constant variable.

2. const声明的变量不得改变值，这意味着，const一旦声明变量，就必须立即初始化，不能留到以后赋值。

    const foo;
    // SyntaxError: Missing initializer in const declaration
3. const的作用域与let命令相同：只在声明所在的块级作用域内有效。
4. const声明的常量，也与let一样不可重复声明。

```
var m = "37";
let n = "67";

// 下面再定义会报错
const m = "73";
const n = "76";
//Identifier 'm' has already been declared
```
5. 如果函数内部有const变量,该函数表达式也应该用const来定义?

