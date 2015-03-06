---
layout: post
title: Javascript基本要点
categories:
- Javascript
tags:
- js, javascript, node, qml 
---

## 基本类型和引用类型
*  函数参数都是值传递，不论是基本类型(拷贝内容）还是引用类型（拷贝指针）

*  赋值对于引用类型是拷贝地址, 所以函数内想改函数外变量值 --- 不能用赋值哦，但是可以直接对引用进行操作（这也就是引用和指针的区别：引用可以转换为指向对象的操作）:

```
var v1 = []
var v2 = {};
var v3 = {};
function foo(v1, v2, v3)
{
    v1 = [1];
    v2 = [2];
    v3 = {a:3}
}

foo(v1, v2, v3);
alert(v1); // 空白
alert(v2); // [object Object]
alert(v3.a); // undefined
```

```
var v1 = []
var v2 = {};
var v3 = {a:0};
function foo(v1, v2, v3)
{
    v1.push(1);
    v2.a = 2;
    v3.a = 3;
}

foo(v1, v2, v3);
alert(v1); // 1
alert(v2.a); // 2
alert(v3.a); // 3
```

## javascript函数没有块级作用域

* 即：外层函数可以访问内层函数内声明的变量， 且内层函数可以直接访问外层函数声明的变量, （除非该变量名在内层被重新定义）， 无需像c++lambda一样定义捕捉符[&]

*  所以最清晰的写法是将函数内要用到的变量在函数开头逐个定义，而不是使用时再定义（这个c++等严格的语言不同哦），具体原因见：

```sh
    function rain(){
        var x = 1;
        function man(){
            x = 100;
        }
        man();        //调用man
        alert( x );    //这里会弹出 100
    }
    rain();    //调用rain
```

```sh
    var x = 1;
    function rain(){
        alert( x );        //弹出 'undefined'，而不是1
        var x = 'rain-man';
        alert( x );        //弹出 'rain-man'
    }
    rain();
```

* 未使用var关键字定义的变量都是全局变量:

```
    function rain(){
        x = 100;    //声明了全局变量x并进行赋值
    }
    rain();
    alert( x );    //会弹出100
```

这也是JavaScript新手常见的错误，无意之中留下的许多全局变量。所以还是多加 "var" 吧

## prototype

*  可以近似简单的认为是类的静态成员（共有方法）
*  对象在没有prototype对应属性时使用类的prototype对应属性， 对象有该属性时使用自身属性:

```
function DOG(name){
　　　　this.name = name;
}
var test = function(){
    console.debug("hello js>>!");

    DOG.prototype = { species : '犬科' };
    var dogA = new DOG('大毛');
    var dogB = new DOG('二毛');

    dogA.species = '大猫科';
    console.debug(dogA.species); // 大猫科
    console.debug(dogB.species); // 犬科

    console.debug(DOG.prototype.species) // 犬科
}
```
