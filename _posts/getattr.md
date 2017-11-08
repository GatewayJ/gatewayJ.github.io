### Python-Class   
#### Descriptor

      一个Descriptor是指实现了__get__的类，__set__和__delete__是可选的，如果实现了__get__和__set__，则Data Descriptor,如果只是实现了__get__则称为Non-Data Descriptor
      普通实例操作属性时（ get set del） 都是在这个实例或者object或者他的父类的__dict__ 上进行的，查找的顺序也是实例，类，父类.
      所以相应的Descriptor操作属性就是用__get__，__set__和__delete__方法，而不是通过__dict__属性
           
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

http://blog.csdn.net/huithe/article/details/7484606
https://www.zhihu.com/question/25391709
