#### package.json文件配置
###### npm run start一次执行多个指令
- 安装npm-run-all 库
```
yarn add npm-run-all --dev
npm install npm-run-all --save -dev
```
```
 "scripts": {
    "dev:rm": "rm -rf build",
    "start": "npm-run-all --parallel dev:**",
    "dev:client": "node proxy.js",
    "dev:server": "nodemon server.js --exec babel-node --presets es2015,stage-0"
  }
```