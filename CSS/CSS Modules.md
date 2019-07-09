### css-modules
[TOC]
[阮一峰教程链接](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)
##### 局部作用域
CSS Modules的做法就是使用一个独一无二的类名,产生局部作用域
- webpack配置
```
module: {
  loaders: [
    // ...
    {
        test: /\.css$/,
        loader: "style-loader!css-loader?modules"
    },
  ]
}
```
##### 全局作用域
CSS Modules 允许使用:global(.className)的语法，声明一个全局规则。凡是这样声明的class，都不会被编译成哈希字符串。
- css
```
    .title {
        color: red;
    }
    :global(.title){
        color: greenyellow;
    }
```
- html
```
    import style from './App.css';

    export default () => {
        return (
            <h1 className={style.title}>
            Hello World
            <span className="title">全局</span>
            </h1>
        );
    };
```
- 构建工具会将类名style.title编译成一个哈希字符串。
```
    <h1 class="_3zyde4l1yATCOkgn-DBWEL">
        Hello World
    </h1>
    //结果:h1标题显示为红色,span内容显示为绿色    
```
##### 定制哈希类名
    css-loader默认生成hash值,在webpack.config.js里可以配置生成的类名
```
module: {
  loaders: [
    // ...
    {
      test: /\.css$/,
      loader: "style-loader!css-loader?modules&localIdentName=[path][name]---[local]---[hash:base64:5]"
    },
  ]
}
//编译成的哈希类名为demo03-components-App---title---GpMto
```
