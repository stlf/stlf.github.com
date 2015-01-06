Nodejs 学习笔记
---
## 模块
> 文件就是模块， 可以用require通过路径引入, 用exports导出公开函数和属性
'''
var foo1 = require('./foo');
var foo2 = require('./foo.js');
'''
'''
exports.create = function (name) {
...}
'''
> 一个模块中的JS代码仅在模块第一次被使用时执行一次
> 通过命令行参数传递给NodeJS以启动程序的模块被称为主模块
> 二进制模块文件扩展名是.node 

## 包
> 多个子模块组成的大模块称做包，并把所有子模块放在同一个目录里
> 当模块的文件名是index.js，加载模块时可以使用模块所在目录的路径代替模块文件路径, 用package.json也可以指定目录包和主模块名，从而无需index.js也可以像使用模块一样使用包

## 命令行程序
> 就是js脚本

## NPM
> 可以在线下载包(可以在@后指定版本)至模块目录
'''
$ npm install argv@0.0.1
'''
> 可以在线下载命令行程序至模块目录
'''
$ npm install local-web-server -g
'''