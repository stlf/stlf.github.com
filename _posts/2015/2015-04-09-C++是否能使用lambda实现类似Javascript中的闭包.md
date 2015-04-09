---
layout: post
title: C++能使用Lambda实现类似Javascript中的闭包吗？
categories:
- C++
tags:
- C++, Javascript, Lambda
---

### Javascript中的闭包
直接用代码吧：
```
function a() {
    var i = 0;
    function b() {
        ++i;
        return  i;
    }
    return b;
}
var c = a(); // i = 1
c(); // i = 2
```
这是一段很典型的Javascript闭包代码。
### C++中尝试使用类似代码
```
std::function<int()> a(){
    int i = 0;
    return [&](){
        return ++i;
    };
}
...
var c = a(); 
c(); // crash！
```
编译没问题！但是运行到c()时宕机了。

### 结论
- C++不能使用类Javascript中的闭包机制。原因是，C++标准规定：
> The C++ closures do not extend the lifetimes of the captured references

-  而Javascript中的无块级作用域成就了其闭包特性
>  Javascript是一个MagicLanguage, 例如其可以用闭包实现类似类成员属性的特性
