# 	Java基础



## 1、DAO模式和接口

### ①接口的作用

Java中的接口类只是一个外表，接口的实现类才是真正的声明接口时如何工作的。当一个接口被实现之后，该接口实现类就是一个普通的类，就可以被创建和使用。

### ② dao模式

Java中的模式：Java中的模式是指在面向对象的设计过程中用于解决特定问题的套路

dao（Data Access Objects数据存取对象）模式是指位于业务逻辑和持久化数据之间对持久化数据的访问，通俗的来讲就是将对数据库的各种操作封装起来

DAO模式的优势：

1) 隔离了数据访问代码和业务逻辑实现代码。当业务需要使用数据的时候，只需要调用DAO方法即可，完全感觉不到数据库的存在。分工明确。数据访问层的代码不会影响业务逻辑代码的实现，这符合单一职能的原则，降低了耦合性，提高了可复用性。

2) 采用了面向接口的编程，隔离了不同数据库的实现，如果底层的数据库发生变化，如有Mysql变为Oracle只要增加新的DAO接口的实现类即可。原有的Mysql的DAO接口实现类可以不用更改。降低了代码的耦合性同时提高了代码扩展性和系统的可移植性

   

DAO模式的组成

* 1、DAO接口：DAO接口中将所有对数据库的操作定义为抽象的方法。
* 2、DAO接口实现类：针对不同的数据库给出DAO接口定义方法的具体实现。
* 3、实体类：用于存放与传输对象数据。
* 4、数据库连接和关闭的工具类：避免数据库连接和关闭代码的重复使用，方便修改。

## 2、事务

### (1) 事务的定义

事务(Transaction)，事务一般是指将要做的事情。在计算机术语中是指访问数据库并可能更新各个数据项的一个程序执行单元(unit).事务通常由操纵语言或编程语言书写的用户程序的执行所引起。

## 3、 MVC设计模式

1）MVC设计模式分为视图(view)、模型(model)和控制器(controller)

![](C:\Users\lenovo\Desktop\Spring\Spring-notes\img\7.png)

①视图

视图主要是为了与用户进行交互，所使用到的主要使CSS/HTML等前端技术

②模型

模型主要是为了各个功能的实现

③控制器

控制器负责将视图和模型一一对应起来。相当于一个模型分发器。所谓的分发就是：1、接受请求，并将该请求跳转（转发、重定向）到模型进行处理。2、模型处理完成之后，再通过控制器，返回给视图中的请求处。

## 4、Java中的集合

Java中使用集合是为了可以处理一组相似的数据。

在Java中，如果一个对象内部可以持有若干其他对象，并且对外提供访问接口，我们就可以把这种对象成为集合。

集合类主要以下三种

* List 一种有序的列表的集合
* Set 一种没有重复元素的集合
* Map 一种通过键值查找的映射表集合

### 1)、 HashMap

HashMap的底层数据结构是哈希表。

HashMap是线程安全的。

* 线程安全：在Java中，并发是由多线程实现的，在jvm中，各个线程之间互不相干，为了尽可能的提高程序性能，jvm就使用多线程。
* 随着多线程的出现，也就出现了线程安全问题，所谓的线程安全问题最典型的就是死锁和脏数据。简单来说，线程安全问题就是在多线程的环境之中，永远保证程序的正确性。

#### (1)、HashMap的数据结构：

HashMap是一个多维数组和多个单向链表的集合体。

#### (2) 、HashMap的存取原理----调用map.put(k,v)方法

* 先将(k,v),封装成Node节点对象
* 底层调用Hash Code方法，计算出k的int型Hash值
* 拿到k的哈希值，通过哈希算法，将其转换成数组的下标。
* 拿到下标后，如果数组下标位置上没有链表，就把Node对象添加到这个位置上。
  如果下标处有链表，此时会拿着Node对象的k和链表中的每一个节点的key，用equals()方法进行比对，如果发现key有相同的，直接用Node对象的v覆盖掉原来旧的value。如果比完了该链表，发现没有key相同的节点，直接存储在该链表的末尾位置。

## 5、Rest和Restful风格

Rest(Representational  State Transfer) 表述性状态转移：Rest的本质是通过URL(统一资源定位器)来访问资源的一种方式。Rest是面向资源的，服务端将内部资源发布为Rest服务，客户端通过URL使用HTTP协议访问他们

*** Rest原则***

* 网络上所有的事务都被抽象为资源
* 每个资源都有唯一的URL(资源标识符)
* 同一资源具有多种表现形式，通常使用的json形式，通过URL获取到Json形式的资源之后，再通过前端进行渲染。
* 对资源的各种操作不会改变资源标识符
* 所有的操作都是无状态的

*** Restful***

Restful是遵守了Rest原则的web服务。Restful其实就是Rest式的应用。restful其实是由rest派生出来的。

![](C:\Users\lenovo\Desktop\Markdown-image\Java-image\2022-02-28_233603.png)

wrapper概念，动态SQL。json数据格式, @ConrollerAdvice 注解

## 6、映射

### 01、映射的概念

在Java中除了int等基本类型之外，其他的类型全部是class，为了获取该种类型（class）的全部信息，JVM在读取到一种class类型的时候就会将其加载近内存，并且JVM会创建一个对应的class实例来获取class类的全部信息。这种获取某一class类型信息的方式就被成为映射。

例如：在加载String类的时候，JVM会将String.class 文件加载进内存，然后为String类创建一个实例，并将该实例和String关联起来。

``` java
Class cls = new Class(String);
```

JVM所持有的每一个实例对象实际上就是指向一个数据类型。

映射其实就是从已经创建好的类中获取其中的属性和方法。

## 7、Java虚拟机(JVM)

## 8、泛型

### 1)、什么是泛型又名参数化类型

在使用ArrayList的时候，为了保证对数据的存入和取出不出错，为每一种类声明一种ArrayList，但是由于java中的class太多，为了简化开发，就可以使用泛型。所谓的泛型就是定义一种模板，例如ArrayList<T>,其中T可以是任何一种class。然后再代码中为使用到的类创建对应的ArrayList<类型>

使用泛型的好处是不必对类型进行强制转换，它同各国编译器对类型进行检查

### 2）java中泛型的特点

在java中泛型的实现方法是由擦拭法实现的。所谓的擦拭法是指虚拟机对泛型一无所知，所有的工作全部是由编译器做的。对于同一个泛型类，编译器看到的代码中的数据类型是***T***,而虚拟机看到的代码中的数据类型为Object。Java的泛型是由编译器在编译的时候实行的，编译器内部永远把泛型***T***视为Object进行处理，在需要转型的时候，编译器会根据T的类型自动为我们实现安全的强制转型。

### 3） 泛型的三种使用方式

泛型类、泛型接口和泛型方法

## 9、Java的优点

* 简单易学 
* 面向对象
* 支持网络网络编程-Java就是为了简化网络编程而出现的。网络编程也即套接字编程，是为了实现多台计算机之间相互交换数据。
* 平台无关性，多线程
* 可靠性，安全性，编译和解释并存。

## 8、JVM---JDK---JRE

JVM: 是用于运行Java字节码的虚拟机，JVM针对不同的平台都有特定的实现，实现不同平台JVM的目的是使用相同的字节码，在不同的平台上都可以得到相同的运行结果。

* 字节码就是经过javac编译过后的.class文件。

JRE：JRE是java的运行环境，它包括，java虚拟机、java类库等一些基础构建，他能够运行已经编译好的java文件。但是不能创建和编译新程序。

JDK：JDK是指Java开发环境，它拥有JRE所拥有的一切，初次之外，JDK还 包含javac和一些工具，能够编译和创建新的java程序。

Java程序的执行过程：

* .java文件经过javac的编译生成.class 文件
* JVM中的类加载器会首先加载字节码文件，然后通过解释器逐行的解释执行。但是这样会导致执行的速度比较慢。所以后来引入了JIT，JIT属于运行时编译，当JIT完成第一次编译之后，会将一些字节码对应的机器码保存起来，下次使用到使用到这些字节码的时候直接使用机器码。

通过上述的java'程序的执行过程，我们就可以知道，java之所以被称为"编译与解释共存"是因为java程序的执行过程需要先经过编译，然后再解释执行。

JIT： JIT是为了针对java程序中一些可能被重复调用的函数和代码块。当对一个方法代码块第一调用的时候，JVM会使用解释器，并同时为这个方法代码快设置一个阈值。当这个阈值变为零（频繁调用该代码块），就会启动JIT。启动JIT之后就不会对该代码块进行解释，而是进行编译，并保留编译好的机器码用于下一次运行。

## 10、Java和C++的区别

* java和C++ 都是面向对象的语言，都支持继承，重载，封装
* java不提供指针直接访问内存，程序内存是安全的
* C++支持类的单重和多重继承，但是java只支持单重继承，但是java接口支持多重继承。
* java中具有垃圾回收机制，不用程序员手动回收垃圾
* C++ 支撑方法重载和操作符重载，但是java只支持方法重载。

## 11、静态方法和动态方法

静态方法在类被加载的时候就会被分配内存，在整个程序的运行期间都会存在于内存之中，特点是运行速度快，所以静态方法是哪些常被访问的方法。

动态方法只有当方法所在的类被实例化之后才能进行访问，特点是执行速度慢

## 12 、Java中的equals和==的区别

java中的值传递和引用传递：

* 值传递：方法接受的实参的值的拷贝，会创建副本

* 引用传递：方法接收的是实参对象在堆中的地址，不会创建副本，对形参的改变将会影响到实参。







Java中只有值传递，因此对于基本数据类型和引用数据类型，使用==实际上比较的都是值，但是对于基本数据类，双等号实际上比较的就是数值，但是对于引用数据类型来说，**双等号就是比较的地址**。

equals不能用于判断基本数据类型的变量，只能用来判断两个对象是否相等，equals存在于每一个类中

* 类没有重写equal方法的时候，默认通过双等号来判断这两个对象是否相同
* 一般都是重写equals方法，equals方法被重写之后，一般用于判断两个对象中的属性相等，如果相等则返回true，即认为这两个对象相等。

重写equals方法的时候，一般还需要重写Hashcode方法，HashCode方法的目的是获取哈希码。在没有重写的情况下，该方法可以将**变量内存地址转化为整数之后返回**。如果在重写euqals方法之后没有重写HashCode方法，就会导致使用equals判断是两个相同对象的情况下，HashCode 的值却不相等。但又必须要求两个相等的对象其HashCode的值必须要相等。所以重写equals的方法的时候必须要重写HashCode方法。

HashSet中加入一个对象的过程：

* 首先会计算HashCode 的值来判断对象加入的位置，然后再与已加入的对象的HashCode值进行比较，如果没有相等的值就会将该对象加入。如果有相等的值，但也有可能是哈希冲撞，因此需要使用equals方法判断两个对象是否相等。如果equals的返回值是true，则拒绝该对象的加入，如果为false，则重新散列到其他地方。

## 13、Java中的基本数据类型及其包装类

Java中的基本数据类型都存在于Java虚拟机栈中的局部变量表中。

Java中的每一个基本数据类型都对应一个包装类。包装类的主要作用有以下两个

* 在某些设计到对象操作的时候，不可使用基本数据类型，但是可以使用包装类。如List<int>不合法但是List<Integar>却是合法的。

### 自动装箱和拆箱

* 装箱：将基本数据类型与他们对应的应用类型包装起来。
* 拆箱：将包装类型转化为基本数据类型

~~~ java
Integar i = 10;// 装箱
int n = i;// 拆箱
~~~

## 14、栈内存和堆内存

* 栈内存：存放基本数据类型和对象的引用和方法的调用。栈中的数据可以共享，存储速度快。
* 堆内存：存放new出来的对象和数组，在进行分配之前会事先从操作系统中获取一个存取空闲块记录的链表，然后从链表中找出第一个大于分配内存的空闲块，将其分配给程序，并更新空闲块表



## 15、成员变量和局部变量

成员变量和局部变量的区别

* 语法形式：局部变量不可以被除final以外的访问修饰符修饰。成员变量可以被修饰

* 存储形式：被static修饰的成员变量是属于类的，没有被static修饰的是属于实例的。而对象存储在堆中。局部变量存储在栈内存中

* 生存时间：成员变量随着对象的创建而创建，随着对象的消失而消失。而局部变量随着方法的调用而消失

* 默认值：成员变量如果没有被赋予默认值，则会自动以类型的默认值而赋值。而局部变量不会自动赋值。但是被final修饰的局部变量也必须被强制赋值

对象的相等一般是指内存中存放的内容是否相等。引用的相等一般是指引用指向的内存地址是否相等

构造方法的作用主要是完成类的初始化工作。构造方法不能被重写，但是可以被重载。重载一定要求参数列表不一样

## 16、面向对象的三大特征

### 1）、封装

封装是指Java将一个对象的属性隐藏在对象内部，外部对象无法直接访问，但是可以通过对象的提供的一些外部访问方法进行访问。

### 2）、继承

### 3）、多态

多态指的是一个引用变量到底指向哪个类的实例对象，该引用变量发出的方法调用调用的到底是哪个类中的方法，必须由程序在运行期间才能确定，因为程序在具体运行时才能确定具体的类.

假设酒是一个父类，其子类由剑南春（JNC），茅台，五粮液等。我们在实现引用的时候通过酒这一个父类就可以实现对所有子类的引用。即

酒 b = 五粮液

酒 c = 茅台

酒 d = 五粮液

只有在具体运行时候我们才知道到底是引用的哪一个类。

在实现多态的时候使用到了向上转型。下面可以通过一个例子来理解向上转型

Wine a = new JNC（）；

我们可以这样理解上面的代码，首先我们声明了一个Wine类型的a 也就是所有酒的父类。a执行JNC实例。由于JNC是属于WIne的子类。所以JNC自动向上转型为Wine，所以a是可以执行JNC对象的。这样做我们就可以使用到子类强大的功能。父类类型的引用可以调用父类中调用的一切方法和属性，但是对于只存在于子类中的方法和属性，该引用就无法调用。

## 17、抽象类和接口

一个包含抽象方法的类就是抽象类，抽象类就是为了继承而存在的，抽象类中的抽象方法需要在子类中进行具体实现。如果一个类继承一个抽象类，则必须实现父类中的方法，否则该类也是一个抽象类。

* 抽象类中方法并不一定全部都是抽象方法，但是一个接口中的方法必须都是抽象方法。
* 接口中的成员变量必须都是 public static final 类型，但是抽象类中的成员变量可以是各种类型的。

##  18、深拷贝、浅拷贝和引用拷贝

### 1）、浅拷贝

浅拷贝会在堆上创建一个新的对象，如果被拷贝对象内部有引用类型（内部对象）的话，浅拷贝只会复制内部对象的地址，也就是说拷贝对象和被拷贝对象公用一个内部对象地址

### 2）、深拷贝

深拷贝和浅拷贝不同的是会复制整个对象，包括这个对象的内部对象

### 3）、引用拷贝

引用拷贝就是将两个不同的引用指向同一个对象

<img src="C:\Users\lenovo\Desktop\Markdown-image\Java-image\shallow&deep-copy.08611c43.png" style="zoom:50%;" />

## 19、Java中的反射机制

Java中创建一个对象是通过new实现的，将一个类的java文件编译成.class文件，就相当于创建了一个对象。.Class文件中包含一个对象的所有的属性和方法。反射和创建一个对象的过程正好是反着来。所谓的反射机制就是从.Class文件中获取到对象的方法和属性。所以为了实现反射机制，就必须先获取.class 字节码文件。获取一个类的字节码文件主要有以下三种方式：

* Class.forName("类的完整路径")
* 对象.getClass()
* 类名.Class

### Java中的静态代理和动态代理

代理始终设计模式：代理模式给一个对象提供一个代理对象，通过这个代理对象，可以控制对原对象的引用，代理对象就相当于一个中介，通过这个中介可以帮我调用原对象的功能，在使用原对象功能的同时还可以扩展功能。

#### 静态代理和动态代理的区别

静态代理需要程序员手动编写或自动生成代理类，在程序编译的时候就会生成对应的.class的文件。静态代理需要提前创建代理类，并在编译的时候事先创建代理对象。

动态代理则不需要提前创建代理对象，只需要提供一个动态创建器，程序在运行的时候会自动生成代理类。



## 20、 异常

异常的结构：

<img src="C:\Users\lenovo\Desktop\Markdown-image\Java-image\types-of-exceptions-in-java.62f25be2.png" style="zoom:50%;" />

Exception 和Error都是继承与throwable 类。不同的是Exception是程序本身可以处理的异常，可以通过Catch进行不会。Error是程序本身无法处理的错误，不可以可以通过catch进行捕获，一般会选择线程终止。在EException中又有受检查的异常和不受检查的异常。受检查的异常必须经过程序处理，不受检查的异常可以不经过程序的处理。

### （1）、受检查的异常和不受检查的异常之间的区别

受检查的检查的异常如果没有经过catch进行捕获处理的话，就无法通过编译。

### （2）try catch finally 的使用

try用以捕获异常，catch块用以处理捕获的异常，try后可以接多个catch块

finall中的语句并不一定会执行。在以下三种情况下 finally中的语句并不会被执行

* JVM终止
* 线程死亡
* 关闭CPU

## 21、I/O

### （1）、什么是持久化

持久化就是将内存中的数据保存起来，并使之长期存在。在Java中，我们可以将Java对象直接保存在文件中，在需要使用的时候直接从文件读取，这也是对象持久化的一种方式。

### （2)、序列化和反序列化

在持久化Java对象的过程中，我们需要使用到序列化和反序列化。

* 序列化：将数据结构和对象转化成二进制流的过程，序列化的主要作用是通过网络传输对象或者将对象存储到数据库，文件系统和内存之中。
* 反序列化：将二进制流转化成数据结构和对象的过程

### （3）、I/O流的种类

* 按照方向划分，分为输入流和输出流

* 按照操作的单元划分，可以分为字节流和字符流。

  *  为什么有了字节流还需要字符流
    * 因为字节转化成字符非常耗时，而且很容易出现编码问题。如果只有字节流，就必须需要经历这个转换，所以为了避免出现上述问题，就将字符里作为一个单独的部分，从而提高了字符流的使用效率。

* 按照流的角色划分可以划分为节点流和处理流

  * 节点流：可以从或向一个特定的设备读写数据
  * 处理流：程序通过一个间接流类去调用一个节点流类，这个间接流类就是处理流。

  ### （4）、I/O模型详解

  #### Java 中常见的三种I/O方式

  * BIO（Blocking I/O）同步阻塞I/O模型：在该模型中，当应用程序发起read调用的时候，就会一直阻塞，直至内核将数据存放到用户空间之中。I/O请求较小的请求下该模型适用，但是在高流量的请求下，该模型就不行了
  * NIO（Non-blocking I/O），该I/O模型提供面向缓冲，面向通道的I/O操作方法，对于高并发的应用，应该使用NIO
    *  同步非阻塞型I/O采用了轮询机制，在数据为准备好期间线程不会被阻塞，并同时采用轮询机制查询数据是否准备好，当数据准备好之后，线程被阻塞，然后开始向用户空间拷贝数据。但是轮询的过程是十分耗费CPU资源的。
    * <img src="C:\Users\lenovo\Desktop\Markdown-image\Java-image\2.jpg" style="zoom:50%;" />

  

  * 为了解决同步非阻塞性I/O的问题。多路复用技术又出现了。在I/O多路复用模型之中，线程首先发起select调用。询问内核数据是否就绪,。等内核将数据准备好了，内核会向系统返回ready，然后程序再发起read调用。
  * <img src="C:\Users\lenovo\Desktop\Markdown-image\Java-image\2022-03-20_175317.png" style="zoom:50%;" />

* AIO(Asynchronous I/O) 异步I/O
* <img src="C:\Users\lenovo\Desktop\Markdown-image\Java-image\4.jpg" style="zoom:50%;" />

## 22、Java中的值传递

实参和形参之间的值传递有两种方法：引用传递和值传递

* 值传递：将实参的值直接复制一份给形参传递到函数中去。这样在函数中对参数进行更改不会影响到实际参数。创建副本
* 引用传递：指在函数的调用过程中将实际参数的地址直接传递到函数中，这样在函数中对参数做的改变将会影响到实际参数。不创建副本

在Java中只有值传递。当形参是一个对象的时候，Java会将实参的地址复制一份传递给形参。区分值传递和参数传递关键是看实参传递给形参的值 是否发生改变。

当传递函数的是实参的地址时，即使函数改变了对象中的某一个属性，但是传递给形参的地址值并未发生改变，其仍然是值传递。如下面的例子

~~~ java
import java.lang.Integer;
public class UTFVerify{
    public static void main(String args[]) {
      User hollis = new User();
      hollis.setName("hollis");
      hollis.setEmail("daskjdlka");
      pt.pass(hollis);
      System.out.println(hollis);
    }
    public void pass(User user){
      user.setName("hollischuang");
      System.out.println(user);
    }
}
~~~

上述代码的输出为：name = hollischuang     name = hollischuang

这样乍一看起来时引用传递，但实际上是值传递，传递到函数中的值实际上是实参的复制的地址。下图为上述代码的执行过程

<img src="C:\Users\lenovo\Desktop\Markdown-image\Java-image\v2-894124b2b6f6a2e77698f20b90c84f95_r.jpg" style="zoom:50%;" />

所以Java中只有值传递。[参考文章地址](https://www.zhihu.com/question/31203609/answer/576030121)

## 23、Java中的静态代理和动态代理

### JDK 动态代理

静态代理和动态代理的区别：静态代理需要实现接口实现类中的全部方法，但是动态代理只需要根据需求实现特定的方法。

静态代理实现的步骤：

* 定义一个接口及其实现类

~~~ java
public interface SmsService {
    String send(String message);
}// 定义一个接口、


//接口的实现类
public class SmsServiceImpl implements SmsService {
    public String send(String message) {
        System.out.println("send message:" + message);
        return message;
    }
}
~~~



* 创建一个代理类同样实现该接口

~~~ java
public class SmsProxy implements SmsService {

    private final SmsService smsService;

    public SmsProxy(SmsService smsService) {
        this.smsService = smsService;
    }//类的有参构造器
    
   // 代理类中重写了原来类中的方法
    @Override
    public String send(String message) {
        //调用方法之前，我们可以添加自己的操作
        System.out.println("before method send()");
        smsService.send(message);
        //调用方法之后，我们同样可以添加自己的操作
        System.out.println("after method send()");
        return null;
    }
}
~~~



* 将目标对象注入代理类，并在代理类中调用原对象的方法。

~~~java
public class Main {
    public static void main(String[] args) {
        //创建一个接口实现类对象
        SmsService smsService = new SmsServiceImpl();
        //将创建后的对象注入代理类中，通过代理类实现对原来类中各个方法的访问。
        SmsProxy smsProxy = new SmsProxy(smsService);
        smsProxy.send("java");
    }
}
~~~

动态代理的实现过程：

* 创建一个接口及其实现类

~~~ java
public interface SmsService {
    String send(String message);
}


public class SmsServiceImpl implements SmsService {
    public String send(String message) {
        System.out.println("send message:" + message);
        return message;
    }
}
~~~



* 自定义 `InvocationHandler` 并重写`invoke`方法，在 `invoke` 方法中我们会调用原生方法（被代理类的方法）并自定义一些处理逻辑；

~~~ java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

/**
 * @author shuang.kou
 * @createTime 2020年05月11日 11:23:00
 */
public class DebugInvocationHandler implements InvocationHandler {
    /**
     * 代理类中的真实对象
     */
    private final Object target;

    public DebugInvocationHandler(Object target) {
        this.target = target;
    }

    //在动态代理中，通过代理类去调用原生方法的时候实际上调用的invoke函数，通过invoke去调用在其中的原生方法。
    public Object invoke(Object proxy, Method method, Object[] args) throws InvocationTargetException, IllegalAccessException {
        //调用方法之前，我们可以添加自己的操作
        System.out.println("before method " + method.getName());
        Object result = method.invoke(target, args);
        //调用方法之后，我们同样可以添加自己的操作
        System.out.println("after method " + method.getName());
            return result;
    }
}

~~~



* 通过 `Proxy.newProxyInstance(ClassLoader loader,Class<?>[] interfaces,InvocationHandler h)` 方法创建代理对象；

~~~ java
//该类的实现实际上是通过反射机制实现的。
public class JdkProxyFactory {
    public static Object getProxy(Object target) {
        // 返回一个代理类对象
        return Proxy.newProxyInstance(
                target.getClass().getClassLoader(), // 目标类的类加载
                target.getClass().getInterfaces(),  // 代理需要实现的接口，可指定多个
                new DebugInvocationHandler(target)   // 代理对象对应的自定义 InvocationHandler
        );
    }
}

// 动态代理类的实际使用
//实现的过程------当创建一个新的接口实现类之后，将其传给getProxy方法，在该方法中，利用反射机制可以获取到原来类中需要实现的各种接口
//然后将这些类放入到代理中进行特定的实现，这样就创建了一个代理类对象。就可以通过代理类对象对原类中的方法进行调用。
SmsService smsService = (SmsService) JdkProxyFactory.getProxy(new SmsServiceImpl());
smsService.send("java");
~~~

### CGLIB代理

JDK 代理一个致命的缺点就是只能代理实现了接口的类。对于没有实现接口的类则不能进行代理。而CGLIB代理则可以避免上述的问题。

CGLIB是一个基于ASM的字节码生成库，它允许我们在运行时对字节码进行是对字节码修改和动态生成。

CGLIB实现动态代理的步骤

* 定义一个类

~~~ java
public class AliSmsService {
    public String send(String message) {
        System.out.println("send message:" + message);
        return message;
    }
}
~~~



* 自定义 `MethodInterceptor` 并重写 `intercept` 方法，`intercept` 用于拦截增强被代理类的方法，和 JDK 动态代理中的 `invoke` 方法类似；

~~~ java
import net.sf.cglib.proxy.MethodInterceptor;
import net.sf.cglib.proxy.MethodProxy;

import java.lang.reflect.Method;

/**
 * 自定义MethodInterceptor
 */
public class DebugMethodInterceptor implements MethodInterceptor {


    /**
     * @param o           代理对象（增强的对象）
     * @param method      被拦截的方法（需要增强的方法）
     * @param args        方法入参
     * @param methodProxy 用于调用原始方法
     */
    @Override
    public Object intercept(Object o, Method method, Object[] args, MethodProxy methodProxy) throws Throwable {
        //调用方法之前，我们可以添加自己的操作
        System.out.println("before method " + method.getName());
        //调用原始的方法
        Object object = methodProxy.invokeSuper(o, args);
        //调用方法之后，我们同样可以添加自己的操作
        System.out.println("after method " + method.getName());
        return object;
    }

~~~



* 通过 `Enhancer` 类的 `create()`创建代理类；

~~~ java
import net.sf.cglib.proxy.Enhancer;

public class CglibProxyFactory {

    public static Object getProxy(Class<?> clazz) {
        // 创建动态代理增强类
        Enhancer enhancer = new Enhancer();
        //以下代码都是通过反射机制实现
        // 设置类加载器
        enhancer.setClassLoader(clazz.getClassLoader());
        // 设置被代理类
        enhancer.setSuperclass(clazz);
        // 设置方法拦截器
        enhancer.setCallback(new DebugMethodInterceptor());
        // 创建代理类
        return enhancer.create();
    }
}



//实际使用过程
AliSmsService aliSmsService = (AliSmsService) CglibProxyFactory.getProxy(AliSmsService.class);
aliSmsService.send("java");
~~~

# Java进阶

## 1、容器

java中的结合也叫做容器，主要是由两大接口派生而来，一个是Collection接口，主要用于存放单一元素，另一个是Map接口，主要用于存放键值对，Collection下主要有三个子接口：

* List：存储的元素是有序的（按存放时间有序），可重复的。
* Set：存储的元素是无序的，不可重复的
* Queue：按特定的排队队则来决定先后顺序，元素是有序的，可重复的。

另外，Map中是使用键值对对数据进行存储的，其中键key是无序的不可重复的，值value是无序的，可以重复的。

### 1）、List

ArrayList和Vector的区别

* ArrayList是List的主要实现类，底层使用数组进行实现，适用于进行频繁的查找工作，线程不安全
* Vector是List的较早实现类，底层也是基于数组进行实现的，线程是安全的。

ArrayList和LinkedList的区别

* 两者都不是线程安全的
* 前者是基于数组，后者是基于双向链表
* 插入与删除元素的速率
* 随机访问
* 空间占用
