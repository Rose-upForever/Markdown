# 1、基础学习

## 1、列表（List）

### 1、sort()和sorted()函数的区别

sort和sorted函数都是实现对列表进行排序的函数，但是sort函数实在原有列表的基础上对列表进行排序，并不会生成一个新的列表。但是sorted函数对列表进行排序是返回一个新的列表。

## 2、可变数据类型和不可变数据类型

### 1、可变数据类型

当数据类型对应的变量的值发生改变的时候，对应的内存地址不会发生改变，对于这种数据类型我们称之为可变数据类型.通俗点说 为该数据类型声明的变量所分配的内存空间中存储的值是可以被改变的

但是结合set有一个不可变的集合***frozenset***

~~~ 
List、set、numpy 、array 、dictionary
~~~



### 2、 不可变数据类型

当数据类型对应的变量的值发生改变的时候，对应的内存地址发生改变，我们就称之为不可变数据类型。通俗点说 为该数据类型声明的变量所分配的内存空间中存储的值是不可以被改变的。

```
integer`, `float`, `long`, `complex`, `string`, `tuple`元组, `frozenset
```

## 2、面向对象基础和进阶

***把一组数据结构和处理他们的方法称为对象，把相同行为的对象归纳为类，通过类的封装隐藏内部的细节，通过继承实现类的特化和泛化，通过多态实现基于对象类型的动态分配。***

类是对象的蓝图和模板，对象是类的实例

## 3、__init__方法

```py
__init__(self,name,sex)
	self.name = name
	self.sex = sex
```

init函数的主要作用是在实例对象被创建的时候对类中的属性进行初始化，self指的是被创建的实例本身，不用作为参数传入/

## 4、slots方法

slots方法可以限定一个类中只可以绑定哪些属性，但是这个限定对于子类无效

~~~python
class Person(object):

    # 限定Person对象只能绑定_name, _age和_gender属性
    __slots__ = ('_name', '_age', '_gender')

    def __init__(self, name, age):
        self._name = name
        self._age = age
    #getter方法
    @property
    def name(self):
        return self._name

    @property
    def age(self):
        return self._age
    # setter方法
    @age.setter
    def age(self, age):
        self._age = age

    def play(self):
        if self._age <= 16:
            print('%s正在玩飞行棋.' % self._name)
        else:
            print('%s正在玩斗地主.' % self._name)


def main():
    person = Person('王大锤', 22)
    person.play()
    person._gender = '男'
~~~

## 5、类方法和静态方法

在类中我们可以定义定义很多对象方法，也就是这些方法是发送给对象的消息，这些方法需要通过对象来实现调用。但是有时候我们写在类中的方法并不一定都需要是对象方法。例如顶一个三角形类，通过传入三条边来判断这三条边是否可以组成三角形，并提供计算三角形周长和三角形面积的方法，但是在创建三角形对象之前我们需要判断这三条边是否可以组成三角形，这个方法显然就不是对象方法，因为调用这个方法的时候三角形还未完成创建，***所以这个方法属于三角形类但是不属于三角形对象***，可以通过静态方法在类中创建类似的方法。

~~~python
from math import sqrt

class Triangle(object):
    def __init__(self, a, b, c):
        self._a = a
        self._b = b
        self._c = c
    @property
    def a(self):
        return self._a
    @property
    def b(self):
        return self._b
    @property
    def c(self):
        return self._c
    @a.setter
    def a(self, a):
        self._a = a
    @b.setter
    def b(self, b):
        self._b = b
    @c.setter
    def c(self, c):
        self._c = c
    # 定义静态方法，用以表示类中的方法，而不是对象的方法，不可以通过对象进行调用
    @staticmethod
    def is_valid(a, b, c):
        return a + b > c and a + c > b and b + c > a
    def perimeter(self):
        return self._a + self._b + self._c
    def area(self):
        half = self.perimeter() / 2
        return (half * (half - self._a) * (half - self._b) * (half - self._c)) ** 0.5

def main():
    a, b, c = 3, 4, 5
    # 静态方法通过类名进行调用
    if Triangle.is_valid(a, b, c):
        t = Triangle(a, b, c)
        #对象方法通过对象进行调用
        print(t.perimeter())
        print(t.area())
    else:
        print('无法构成三角形')
if __name__ == '__main__':
    main()

~~~

和静态方法一样，类中也可以有类方法，类方法的第一个参数的约定名cls，表示的是当前类相关信息的对象（类本身也是一个对象，有的地方也称之为类的元数据对象），通过这个参数我们可以获取类的相关信息，并创建出类的对象

~~~python
class Clock(object):
    类方法
    @classmethod
    def now(cls):
        ntime = localtime(time())
        return cls(ntime.tm_hour, ntime.tm_min, ntime.tm_sec)
    
 通过类方法创建对象
clock = Clock.now()


~~~

类之间的关系有继承，泛化，依赖三种

### 继承和多态

子类在继承了父类的方法后，可以对父类已有的方法给出新的实现版本，这个动作称之为方法重写（override）。通过方法重写我们可以让父类的同一个行为在子类中拥有不同的实现版本，当我们调用这个经过子类重写的方法时，不同的子类对象会表现出不同的行为，这个就是多态（poly-morphism）。