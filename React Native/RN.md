### React Native
##### 1.JDK安装和环境变量的配置
##### 2.NodeJS环境安装
##### 3.Android SDK环境搭建和环境变量配置
- Android SDK下载，（需要稳定的VPN）。
- 安装需要的包，需要很长时间，并且磁盘剩余空间充足，50G足够。（需要稳定的VPN）
- 环境变量配置

##### 4.RN环境搭建
- 安装react native命令行工具
```
yarn global add react-native-cli
```
- 初始化项目
```js
react-native init NewProject
//NewProject为项目名
```
##### 5.安装Genymotion模拟器

##### 6.RN项目连接模拟器调试
- 在RN项目目录的`android`目录下创建名为`local.propertiesd`的文件
```js
//在文件内添加的内容为
sdk.dir=android sdk的目录路径
```
- 开启react-native服务状态
```js
cd NewProject
react-native start
//该命令会开启一个进程，模拟器和手机会请求这个进程的
//接口来获取数据，再临时封装成一个app将页面显示出来
```

- 另外开启一个dos窗口
adb devices:
查看连接设备信息
 ![alt](../../imgs/adb2.png)
- 连接模拟器,5555是Genymotion的端口号 
adb connect ip:5555
 ![alt](../../imgs/adb3.png)

- 常用adb命令：
adb usb
adb start-server
adb kill-server
adb devices 查看系统是否识别设备(List of devices attached 是没有识别到设备)
##### 运行RN项目
```
react-native run-android
```

