

# 命令行

## 常用命令

```java
切换目录
“cd”是打开目录，改变盘符，直接输
1、从C盘切换到其他盘，D盘、E盘
输入“d:”
2、打开D盘下的某个文件夹
输入“cd test”
3、返回上一级目录
输入“cd ..”
4、回到根目录
输入“cd \”

查看目录内容
输入“dir”

新建、复制、删除目录文件或文件夹
1、输入命令“mkdir”和“md”来创建文件夹
2、输入命令“type nul>*.*”创建空文件，输入命令“echo [fileContent]>*.*”创建费控文件夹
3、输入命令“copy test.txt test3.txt”复制文件
4、输入命令“xcopy D:\test\test1 d:\test\test3 /s /e”复制文件夹
参数“/s”表示子文件一起复制
参数“/d”表示如果目标文件比源文件老才覆盖
5、输入命令“del *.*”删除文件
6、输入命令“rd <folderName>”删除文件夹
```

## 环境变量

path：当在命令行中运行某一程序或打开某一文件时，首先在当前目录下寻找，如果没有找到则会在path中的路径进行查询。



# 进程和线程

## 进程

​	进程负责为程序的运行提供必备的环境

​	相当于工厂中的车间

## 线程

​	计算机中最小的计算单位

​	执行进程中的程序

​	工厂中的工人



# Node.js

## 简介

能够在服务器端运行JavaScript的开放源代码、跨平台的JavaScript运行环境

## 用途

类似于服务器

单线程

## 使用

### 模块化

#### 模块声明和引入

一个js文件就是一个模块

*引入其他模块*

```javascript
require("")   //一般为相对路径
```

使用require（）引入模块以后，该函数会返回一个对象，这个对象代表的是引入的模块

每一个js文件中的js代码都是独立运行在一个函数中，而不是全局作用域，所以一个模块中的变量和函数在其它模块中无法访问

可以通过exports来向外部暴露变量和方法

```javascript
exports.x="x"
```

*示例代码:*

model.js

```javascript
exports.add = function (a, b) {
    return a + b;
}

exports.mul = function (a, b) {
    return a * b;
}
```

test.js

```javascript
let require1 = require("./model");
let add = require1.add(1, 3);
let mul = require1.mul(2, 30);
console.log(add)
console.log(mul)
```

#### 模块标识：

引入外部模块时，使用的就是模块标识

##### 核心模块：

​	由node引擎提供的模块

​	标识为模块名

##### 文件模块：

​	由用户自己创建的模块

​	标识为路径

### node运行

在node有一个全局对象global，它的作用和网页中的window类似

在全局中创建的变量都会作为global的属性保存

在全局中创建的函数都会作为global的方法保存

当node在执行模块中的代码时，他会首先在代码的最顶部，添加如下代码

```javascript
function (exports, require, module, __filename, __dirname) 
```

实际上模块中的代码都是包装在一个函数中执行的，并且在函数执行时，同时传递了五个实参

exports

​	该对象将变量、函数暴露到外部

require

​	函数，用来引入外部模块

module

​	代表的是当前模块本身

​	exports就是module的属性

既可以使用exports导出，也可以使用module.exports导出

__filename

​	当前模块的完整路径

__dirname

​	当前模块所在文件夹的完整路径

### module.exports和exports区别

module.exports和exports

​	exports只能通过.的方式向外暴露变量

​	而module.exports既可以通过.的方式也可以直接赋值

```javascript
//直接修改变量的值（栈）
exports = {
    name :"fourteen",
    age:20,
    sayName:function () {
        console.log("我是"+name)
    }
}
//修改变量所指向的地址中的值（堆）
module.exports = {
    name :"fourteen",
    age:20,
    sayName:function () {
        console.log("我是"+name)
    }
}
```

### 包 package

文件夹

#### 包结构

​	组织包中的各种文件

#### 包描述文件

​	包的相关信息，主要为外部提供

## npm

完成了第三方模块的发布、安装和依赖等

node与第三方模块之间形成了一个很好的生态系统

命令

npm -v

​	查看npm版本

npm version 

​	查看所有模块版本

npm install/i 包名

​	安装包

npm install/i 包名

​	全局安装包（全局安装的包一般都是一些工具）

npm  remove/m 包名

​	删除包

npm install

​	下载当前项目所依赖的包



通过npm下载的包都放到node_modules文件夹中

我们通过npm下载的包，直接通过包名引入即可

在使用模块名来引入模块时，他会首先在当前目录node_modules中

如果有直接使用，如果没有则取上一级目录的node_modules中寻找

如果有则直接使用，如果没有则再去上一级node_modules中寻找

如果到磁盘的根目录还没有则报错

### 配置cnpm

淘宝的镜像让下载包的时候更加快速