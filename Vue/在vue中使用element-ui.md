#### 安装
```
npm i element-ui -S
```
#### 按需引入
- 安装 babel-plugin-component：
```
npm install babel-plugin-component -D
```
- 将 .babelrc 修改为:
```
{
  "presets": [
    [
      "env",
      {
        "modules": false
      }
    ],
  ],
  "plugins": [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```
- 如果你只希望引入部分组件，比如 Button 和 Select，那么需要在 main.js 中写入以下内容：
```
import { Button, Select } from 'element-ui';
Vue.use(Button)
Vue.use(Select)
```