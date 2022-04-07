# 第一天学习笔记

## 1、IoC （控制反转）理解

在传统的模式下，对象的创建’赋值和生命周期的管理的全部是由程序人员进行管理。开发人员对于对象进行全部的控制。在IoC模式下，对于对象的管理全部交给容器进行。Spring就相当于一个容器。我们使用容器中创建的对象。

## 2、IoC的关键要素

#### 1.控制

控制是指对开发人员对对象具有完全的控制，全称掌控对象的创建、赋值和生命周期的管理

#### 2.反转

反转就是将对对象的控制权转交给容器容器进行管理

#### 3. 正转

正转就是指开发人员通过new进行对象的创建和管理。

## 3、IoC实现的关键技术

#### DI（dependency Injection）依赖注入

在原始情况下，当一个对象需要引用另外一个对象中的方法的时候往往需要事先创建该对象.

``` jav
pulic class Human{

pulic void createHuman(){

}

} 

public class Man{

Human H =new Human;
b.createHuaman;

}
```

## 4、Spring的实现过程

1. 创建maven项目

2. 加入依赖，修改Pom.xml文件。主要需要添加的依赖有。

   spring-context：Spring 依赖

   Junit：单元测试依赖

3. 开发人员进行类的定义：往往需要先定义接口然后再定义实现类

4. 创建Spring文件，用以进行对象的生命，将对象交给Spring进行管理。使用<bean>进行声明，一个<bean>就代表一个java对象。

5. 使用容器中的对象。创建一个表示Spring容器的对象AppicationContext。从容器中，根据名称进行对象的获取，使用getBean("对象名称")，进行对象的获取。

## 5、Spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"---s声明命名空间
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"----声明xsi命名空间
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd"-----xsi约束文件在互联网上的路径，该约束文件用以约束该xml文件的写法>

</beans>


spring 配置文件
1）根标签是beans标签
2）beans标签后面所跟的是约束文件说明
3）beans的里面放置bean的声明，bean是指java对象，且该对象是交由Spring进行管理的。
```

# 第二天学习笔记

## 1、使用Spring进行对象创建和管理

1、指定Spring配置文件 Spring配置文件在编译之后会放在target\classes目录之下

2、创建容器对象ApplicationContext 就是一个容器对象接口。

3、从容器中获取对象。使用的是getbean方法，但由于我们想要使用的是一个接口类，所以在使用getbean方法获取完对象之后还要进行强制类型转换。

```java
 someService service= (someService) ctx.getBean("someService");
```

## 2、Spring的一些特点

1、Spring默认的是无参构造方法 使用有参构造方法进行构造的时候会报错。

2、在创建Spring容器的时候，Spring框架会读取Spring配置文件同时进行对象的创建。

```java
ApplicationContext ctx = new ClassPathXmlApplicationContext(config);
```

3、Spring一次会将Spring配置文件中的对象全部创建。

4、Spring可以为任意的类创建对象，只要是可以找到该类的位置

## 2、Java杂记

### 1、什么是Java中的反射机制

反射就是指在运行状态下，所定义的任意一个类的属性和方法，对于任意一个对象能够获取到任意一个方法和属性，这种动态的调用信息和对象的方法的功能就是Java的反射机制。

Java中迭代器的作用：Java中的迭代器是为了更加方便的处理集合中的元素，

### 2、Java中的set、get、toString方法

为了方便使用者对于多个属性的调用，因此创建了实体类，实体类就相当于一个装着多个属性的大罐子。当使用到某个属性的属性的时候，通过这个大罐子就可以实现属性的调用。

由于创建实体类的时候 需要将属性设置为私有，所以为了使用和获得这些属性，就需要get方法。同时为了操作这些属性的值，就需要使用set方法。

toString方法是Object类中的方法，使用toString方法就是为了方便输出。

## 3、DI：给属性赋值

DI分类：（1)  set注入 也叫做设值注入（2）构造注入

Spring调用类的无参构造方法，调用方法创建对象之后给属性赋值

赋值的两种方式：

（1）使用xml配置文件中标签的属性

（2）使用注解

### 1、基于XML的DI

在XML文件中使用标签和属性，完成对象的创建和属性的赋值。

1）set 注入

概念：Spring调用类中的set方法，使用set方法可以完成属性的赋值，推荐使用。

```
简单类型
<bean id="" class="">
    <property name="属性名" value="简单类型" />
    </bean>
    
 引用类型的
  <bean id="myStudent" class="org.example.bao02.Student">
        <property name="age" value="18" />
        <property n
        ame="name" value="张三" />
        <property name="school" ref="myschool" /><!--通过ref中的bean的id 找到已经创建好的对象，将该创建的好的对象及其属性赋值给引用类型school-->
    </bean>
    <bean id="myschool" class="org.example.bao02.School">
        <property name="name" value="北京大学" />
        <property name="address" value="北京市海淀区" />
    </bean>
```

上面代码中的-属性名-应该是对应的set方法，value的值是对应的传进来的参数的值。当一个实体类中没有一个属性但是却有属性对应的set方法，使用set注入也可以正常运行。因为Spring中所使用的属性名实际上是set方法后面的属性名。例如没有email属性 但是setEmail 方法存在，那么在Spring中就可以正常运行。

Spring所调用是Set方法，至于属性对应的set方法实现的具体细节，Spring并不关心。可以自己定义set方法的实现细节。所以对于任意一个带有set方法的类，Spring都可以使用set注入去修改其属性值，比如日期类，使用日期类默认打印的是当前的时间，但是通过set注入，我们找到Date类中的time时间使用set注入我们就可以任意的修改时间。所以对于一些不是由开发人员自主定义的类，我们仍然可以去修改其中的属性。

# 第三天学习笔记

2）构造注入

Spring调用类中有参数的构造方法，在创建对象的同时，给属性赋值。

使用到的是<constructor />标签，

constructor标签内的属性的意义：name 代表的是构造方法中的形参名，index 代表的是形参的位置，形参的位置从左往右依次为0.1.2 ........；value：代表的是给简单数据类型赋的值  ref：代表的是引用数据类型的bean id。

```java
//使用形参名标示形参  
<bean id="myStudent" class="org.example.bao03.Student">
       简单数据类型
       <constructor-arg name="myname" value="张三"/>
        <constructor-arg name="myage" value="18"/>
        //引用数据类型
        <constructor-arg name="myschool" ref="mySchool"/>
    </bean>
      
//不使用形参名，使用形参的位置参数，也可以实现使用constructor 对属性的赋值
      <bean id="myStudent2" class="org.example.bao03.Student">
        <constructor-arg index="1" value="2"/>
        <constructor-arg index="0" value="张三"/>
        <constructor-arg index="2" ref="mySchool"/>
    </bean>
          
          
//省略index，将对属性的赋值的语句按照属性的顺序排好，也可以实现使用构造器对属性的赋值
        <bean id="myStudent3" class="org.example.bao03.Student">
        <constructor-arg  value="张三"/>
        <constructor-arg  value="3"/>
        <constructor-arg  ref="mySchool"/>
    </bean>   
```

只要一个类中含有带参数的构造方法就可以使用构造注入进行赋值,如使用File类中的带参数的构造方法，通过对构造器中的参数进行赋值，就可以获取一个文件，并使用。所以，使用对象赋值方法时不应该局限于自己创建的类，java中原有的类，只要类中有带参数的构造方法就可以进行属性的赋值。

``` java
   <bean id="myfile" class="java.io.File">
        <constructor-arg name="parent" value="D:\Git\Git"/>
        <constructor-arg name="child" value="LICENSE.txt"/>
    </bean>
```

## 1、引用类型的自动注入

概念：Spring可以根据某些规则给引用类型进行赋值，该操作只适用于引用类型。常用的规则主要有：byName和byType两种规则。

①：byName:按照名称注入。java类中引用类型的属性名称和Spring容器中的bean的id名称一样的，并且数据类型也是一样的，这些bean能够赋值给引用类型。并且引用类型的数据类型和Spring中bean标签中的class属于同一个类。

```java
    <bean id="myStudent" class="org.example.bao04.Student" autowire="byName">
        <property name="age" value="18" />
        <property name="name" value="张三" /><!--通过ref中的bean的id 找到已经创建好的对象，将该创建的好的对象及其属性赋值给引用类型school-->
    </bean>
    <!--引用类型按照名称的自动注入,一定要注意在引用类中声明的引用类型的属性名一定要和下面的被引用类的bean id 保持一致-->
    private School school;<!--student类中的引用数据类型的声明-->
        
    <bean id="school" class="org.example.bao04.School">
        <property name="name" value="武汉大学" />
        <property name="address" value="北京市海淀区" />
    </bean>
```





②byType：按照类型注入。Java类中引用类型的数据类型和Spring容器中bean的class值是同源关系的。

若要使用同源关系，那么在配置文件中，同一类型的bean只能够声明一个对象，否则会报错。

同源关系：

①、java中引用类型的数据类型和bean中的class的值是一样的。

```java
 <bean id="myStudent" class="org.example.bao05.Student" autowire="byType">
        <property name="age" value="18" />
        <property name="name" value="张三" />
    </bean>
    <!--引用类型按照类型的自动注入-->
     =========================
      private School school;<!--同一个类-->
     =========================
    <bean id="school" class="org.example.bao05.School">
        <property name="name" value="武汉大学" />
        <property name="address" value="武汉市市海淀区" />
    </bean>
```

②、java中引用类型的数据类型和bean中的class的值是父子类关系。被引用类是父类，bean中的class是子类



③、java中引用类型的数据类型和bean中的class的值是接口和实现类的关系。



# 第四天学习笔记

## 1、IOC的优点

使用IOC可以实现解耦合，也就是说将对 对象的各种操作完全交给Spring容器，当需要切换操作对象的时候，只需要去修改配置文件，源代码不需要进行改动

例如我们在数据操作层使用到的时Mysql的数据库，数据操作的接口实现类中的语句是使用Mysql语句进行编写的，当我们需要更换数据的时候，比如更换为Oracle的数据库，那么接口实现类中的语句就要使用Oracle的语句进行编写。

在普通的修改措施中，我们需要将接口实现类中的所有的语句全部修改为Oracle的操作的语句，并同时修改源代码。但是在Spring框架下，我们可以新创建一个Oracle语句的实现类，并同时在Spring的配置文件中创建这一对象，那么我们就可以减少源代码的修改。

<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\1.png" style="zoom: 33%;" />

***



<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\2.png" style="zoom: 50%;" />

## 2、多个Spring配置文件

* 当一个项目中的类过多的时候，就可能导致Spring的配置文件过大。所以Spring就采取了多个配置文件来解决这个问题。

* 划分多个配置文件的方式 （1） 按照功能模块进行划分，一个模块一个配置文件 （2） 按照类的功能分，比如数据库操作相关的类在一个配置文件。
* Spring对于多个配置文件的管理：常用的是包含关系的配置文件，使用一个总的配置文件，里面有一个import标签包含其他的多个配置文件。

语法格式：

``` xml
总的文件
<import resource="其他配置文件的路径"/>
<import resource="其他配置文件的路径"/>
<import resource="其他配置文件的路径"/>
<import resource="其他配置文件的路径"/>
```

使用通配符进行多个配置文件的导入：可以将多个文件导入标签合并为一个配置文件导入标签。前提是所有的被导入的配置文件具有相同的文件命名规则。同时总配置文件不能包含通配符的范围之内。比如总文件不能叫做spring- .....。

<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\6.png" style="zoom:50%;" />

# 第五天学习笔记

## 1、关于注解的DI

注解的主要作用主要是解释和说明。

基于注解的DI：使用spring提供的注解来实现Java对象的创建和属性的赋值。

注解使用的核心步骤：

* 在源代码中加入注解
* 在Spring的配置文件，加入组件标签。

***

### 1、Component 注解

① *@Component* 注解 表示创建对象，作用和bean标签一样，其对象的创建也是交由spring进行创建，其中有一个value属性，表示创建对象的名称，也就是bean中的id.当没有给value赋值的时候，就会使用默认的对象名称。默认的对象名为 首字母小写的类名。

``` java
@Component(value = "mystudent")

@Component <1--使用默认的类名-->
```

在Spring中使用注解之后，要使这些注解正常使用还需要在Spring的配置文件之中声明组件扫描器，该扫描器会扫描base-package位置中的注解。base-package 代之的是注解所在项目包的包名语法格式：

~~~xml
 <context:component-scan base-package="org.example.bao01"
~~~

然后框架会扫描这个包和子包中的所有类去寻找类中的注解，遇到注解后，会按照注解表示的功能会创建对象并给对象赋值。并将对象放到Spring对象之中，交由Spring容器进行管理。

### 2、其余创建对象的注解

和Component类似的创建对象的注解

1) @Repository :放在dao接口的实现类上面，表示创建dao对象，持久层对象，创建的对象能访问数据库。
2) @Service:放在业务层接口的实现类上面，表示创建业务层对象，业务层对象具有事务额功能。
3) @Controller: 放在控制类的上面，表示创建控制器类对象。属于表示层对象。控制器能够接受请求，并将请求分发给模型进行处理，同时可以将处理后的请求发现是给用户

以上四个注解都可以创建对象，但是Component之外的其他注解有角色说明，表示对象是分层的，对象是属于不同的层，具有额外的功能。以上四个注解的语法格式一摸一样。

### 3、扫描多个包的三种方式

① 多次使用组件扫描器

``` xml
<context:component-scan base-package="org.example.bao01" />
<context:component-scan base-package="org.example.bao02" />
```

② 使用分割符指定多个包.分隔符有 , 和  ;

``` xml
<context:component-scan base-package="org.example.bao01;org.example.bao02" />
```

③当一个包中含有多个包的时候，只需要指定父包的位置。因为Spring会扫描base-package路径下所有的包，包括子包。

### 4 、使用注解给对象赋值

#### 1、简单类型的属性赋值

简单类型的属性赋值使用@Value 

##### 1、简单方式

@Value所放位置

* ***在属性定义的上面，无需set方法，推荐使用***
* ***在set方法的上面***
* ***语法：@Value(value="")value是String类型的，所以其值必须放进引号里面***

``` java
 @Value(value = "张三")
    String name;

    @Value(value = "18")
    int age;

    @Value("张三")
    public void setName(String name) {
        this.name = name;
    }

    @Value("18")
    public void setAge(int age) {
        this.age = age;
    }

```

##### 2、使用外部类属性配置文件给属性进行赋值





①创建类属性配置文件

<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\8.png" style="zoom:50%;" />

myconf.properties文件中的内容

<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\9.png" style="zoom:50%;" />

②Spring总配置文件的配置

``` xml
<!--读取外部的类属性配置文件
property-placeholder:读取properties这样的文件
-->
    <context:property-placeholder location="classpath:/myconf.properties" />
```

③实体类中的配置

语法格式@Value("${key}"):其中的key的值为myconf.properties文件中的属性名。

<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\10.png" style="zoom:50%;" />

实现过程：在程序的运行的时候，Spring会首先读取Spring的总配置文件，在读取到组件扫描器标签时，会自动扫描路径下的所有包，遇见@Component注解的时候会自动创建对象。遇到“读取外类属性配置文件”的标签时候，会将路径下的类属性配置文件中的各种属性，如（myname）进行创建，并存放到Spring容器之中。遇到@Value标签的时候，形如上图的格式，会自动读取Spring容器中对应属性(myname)的值，并将其赋值给其下面的属性(name)。

#### 2、 为引用类型赋值

##### (1)使用@Autowired

@Autowired：Spring框架提供的，用于给引用类型进行赋值，采取的是自动注入原理，支持byName,byType 。默认的是byType。

@Autowired中的属性

* required:boolean类型的属性，默认为true。若该属性为true表示spring在启动的时候，创建容器对象的时候，会检查引用类型是否赋值成功。如果赋值失败，就会终止程序执行并报错。若该属性的值为false，如果赋值失败，程序正常执行，不会报错。引用类型的值是null。

@Autowired 注解书写的位置

* ***在属性定义的上面 无需set方法***
* *** 在set方法的上面***

****



① 使用byType实现自动注入

使用该注解为属性进行赋值的时候，会在容器内拿出一个和引用类型同源的对象将其赋值给对应的属性。

``` xml
<bean id="myschool" class="org.example.bao03.School" >
        <property name="name" value="武汉大学" />
        <property name="address" value="武汉市洪山区" />
</bean>
```

``` java
@Autowired
private School school;
```

如上的代码，Spring读取配置文件之后就会创建对应的School对象，并将其放入Spring容器之中。然后@Autowired就会按照类型将其赋值给对应的引用类型。

****



②使用byName实现自动注入

```java
@Qualifier(value="bean的id") 从容器中找到指定名称的对象，把这个对象赋值给引用类型。
```

![](C:\Users\lenovo\Desktop\Spring\Spring-notes\img\11.png)

****

##### (2)、使用@Resource实现自动注入

@Resource是JDK的注解，其功能也是为了实现自动注入。@Resource采用按名称和按类型两种注入方法，默认的是按名称注入。在实际的使用过程中该注解会先使用byName进行赋值，如果赋值失败会在使用byType

使用位置：

* 在属性定义的上面，无需set方法，推荐使用
* 在set方法的上面。

***语法使用格式:***

~~~ java
@Resource(name = "myschool")
~~~

其中name是已经在容器中创建好的对象的id，也就是bean标签中的id

<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\12.png" style="zoom:50%;" />

# 第3章 AOP面向切面的编程

## 1、传统项目开发所面临的问题

* 业务需求改变时，需要修改源代码
* 可能会导致出现多余的重复代码
* 在一个业务逻辑实现类之中添加多个方法会导致业务逻辑实现不清晰。导致代码的维护和管理出现困难。

## 2、解决方法



#### 1)  代理模式

代理模式就是一个中介。代理模式就是给某一个对象提供一个代理对象，并由代理对象控制对原对象的使用，并且用过代理对象还可以实现额外的功能。在进行业务逻辑调用的时候，就可以直接声明代理对象，而不是声明原对象。

<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\14.png" style="zoom:50%;" />

* Subject:抽象类或者接口，
* RealSubject：被代理类。也可以说业务逻辑接口的具体实现类
* Proxy:代理类

<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\15.png" style="zoom:50%;" />

测试类中的实现：

<img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\16.png" style="zoom:50%;" />

代理的最大有点就是通过创建代理，可以实现对目标方法的调用，并且同时还可以增减一些功能，并保持原有的业务逻辑实现代码不会发生改变。

#### 2) AOP

在使用代理设计模式的时候，若需要增加的功能较多，则可能会出现大量的代码，为此，可以通过AOP解决所出现的问题。AOP就是承担了代理类的角色。



## 3、 AOP的概念

AOP(Aspect Orient Programming)即是指面向切面编程.

切面：切面是指给业务方法所增加的功能。如上面图片中的初始和善后的功能。切面一般都是非业务功能，和业务逻辑无关，并且切面功能一般都是可以复用的。例如日志，事务，权限检查，参数检查等功能。切面即是指附加的功能。

怎么使用AOP思想？

* 在程序开发的之前，需要找出所有的切面(附加功能)
* 考虑切面的功能什么时候执行，在什么地方实行，怎么执行。
* 面向切面编程就是在开发的过程中始终围绕着切面进行开发

AOP的好处

* 可以实现切面的复用
* 可以让开发人员专注业务逻辑的实现。提高开发的效率。

## 4、AOP中的一些术语

* 切面
* 连接点(joinpoint)：连接点实际上是一个连接切面的业务方法。当这个业务方法执行的时候，切面的功能也会执行。
* 切入点(pointcut)：是一个或者多个连接点的集合。表示切面的执行位置。
* 目标对象(target)：为谁增加切面功能，谁就是目标对象。
* 通知(IT术语：增加)(Advcie):用来表示切面功能的执行时间。

AOP的三要素：Aspect、Advice、pointcut。所谓的AOP就是指在Advice的时间，在pointcut的位置，去执行Aspect的功能。

AOP是一个动态的思想，在程序的运行期间，创建代理，使用代理执行方法时，增加切面的功能，代理对象是存在与内存之中的。
