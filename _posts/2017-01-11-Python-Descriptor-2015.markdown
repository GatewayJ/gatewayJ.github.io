---
layout:     post
title:      "Python Descriptor"
subtitle:   " \"something about Descriptor in Python\""
date:       2017-01-11 12:00:00
author:     "JiHW"
header-img: "img/post-bg-2017-1-11.jpg"
tags:
    - Python
---

一个Descriptor是指实现了`__get__ `的类, `__set__` 和 `__delete__` 是可选的,如果实现了 `__get__ `和 `__set__` ,则Data Descriptor,如果只是实现了 `__get__` 则称为Non-Data Descriptor。普通实例操作属性时（ get set del） 都是在这个实例或者object或者他的父类的 `__dict__` 上进行的，查找的顺序也是实例，类，父类.
所以相应的Descriptor操作属性就是用 `__get__` ， `__set__`和 `__delete__` 方法，而不是通过`__dict__`属性

```Python
class Descriptor(object):
    def __init__(self, name):
        self.name = name

    def __get__(self,instance, owner):
        print("通过__get__ function")
        return self.name

    def __set__(self,instance,value):
        print("通过__set__ function")
        self.name = value

class Student(object):
    name = Descriptor("jihongwei")

son = Student()
print(son.name)
son.name = "赋值"
print(son.name)

```
实际上Djangode orm定义字段类型的时候用的技术就是orm.

同时也可以用 `proper()` 来创建Descriptor,这样就不用写两个类了。
```Python
class Son():

    def getfunc(self):
        return "this is get"

    def setfunc(self, value):
        print("this is set")

    def delfunc(self):
        return "this is del"

    desc=property(getfunc, setfunc, delfunc)

son = Son()
son.desc = "asd"
print(son.desc)
```
[知乎链接](https://www.zhihu.com/question/25391709)
