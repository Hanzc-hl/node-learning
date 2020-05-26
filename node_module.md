# node 模块
## 全局模块
在node.js文件中可以随时访问的对象，不需要引用

- process.env 环境变量
- process.argv 执行参数
- __dirname 当前路径
- ...

## 系统模块
需要require(), 但不需要单独下载

- path：用于处理文件路径和目录路径的实用工具
- fs：用于文件读写操作

## 自定义模块
require自己封装的模块

- exports：相当于一个导出的对象
- module: 批量导出
- require
    1. 如果有路径， 就去路径里面找
    2. 没有的话就去node_modules里面找
    3. 再去node的安装目录找

```js
module.exports={
    a:1, b:2
}
```

```js
require('./mod')    // 从当前文件夹中寻找mod
require('mod')      // 从node_modules中寻找mod 
```