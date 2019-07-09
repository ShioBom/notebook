###### 事件循环：JS执行机制
![event loop](https://user-gold-cdn.xitu.io/2017/11/21/15fdcea13361a1ec?imageslim)
- macro-task(宏任务)：包括整体代码script，setTimeout，setInterval
- micro-task(微任务)：Promise，process.nextTick
```
console.log('1');
setTimeout(function() {
    console.log('2');
    new Promise(function(resolve) {
        resolve();
    }).then(function() {
        console.log('3')
    })
    new Promise(function(resolve) {
        console.log('4');
        resolve();
    }).then(function() {
        console.log('5')
    })
})
new Promise(function(resolve) {
    resolve();
}).then(function() {
    console.log('6')
})
new Promise(function(resolve) {
    console.log('7');
    resolve();
}).then(function() {
    console.log('8')
})
setTimeout(function() {
    console.log('9');
    new Promise(function(resolve) {
        resolve();
    }).then(function() {
        console.log('10')
    })
    new Promise(function(resolve) {
        console.log('11');
        resolve();
    }).then(function() {
        console.log('12')
    })
})
//结果：1 7 6 8 2 4 3 5 9 11 10 12
```
> (请注意，node环境下的事件监听依赖libuv与前端环境不完全相同，输出顺序可能会有误差)