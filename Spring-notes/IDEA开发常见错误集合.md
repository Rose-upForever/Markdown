# 1、关于maven中_target_文件夹的错误

问题描述：无法找到的各种类或者Spring的错误。

* target文件夹的作用：target文件夹是项目最终运行编译之后的文件存放位置。在target中的各个文件的相对路径才是最终的路径。在某一个配置文件或者类文件已经在项目中存在但是程序运行报错无法找到该文件，就要查看该文件是否已经被放到target目录之下，如果没有放进去，可以将该文件复制到target中的对应位置。

  <img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\3.png" style="zoom: 50%;" />

  * 当将缺乏的文件拖进去无法解决问题的时候，可以采用采取以下方法进行解决

    ①  **点击 IDEA 右侧栏中的 Maven Projects -- 选择你的项目 -- Lifecycle -- clean（清理掉以前的东西） -- compile（重新编译）**

    <img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\4.png" style="zoom:50%;" />

    ② 重新构建项目

    <img src="C:\Users\lenovo\Desktop\Spring\Spring-notes\img\5.png" style="zoom:50%;" />
  
  # 2、swagger错误
  
  spring boot配置完成之后，swagge无法正常访问，出现下列情况

<img src="C:\Users\lenovo\Desktop\Markdown-image\Spring-image\1.png" style="zoom:50%;" />

出现该问题表示无法扫描到swagger配置文件所在的包，需要在启动类之添加@ComponentScan注解，其中的basepackages参数配置为swagger配置文件所在的位置。使用该注解会扫面basepackages 下的所有的包。

# 3、找不到数据库的url配置资源

报错截图：

<img src="C:\Users\lenovo\Desktop\Markdown-image\Java-image\2022-03-12_131910.png" style="zoom:50%;" />

出现上述错无主要有以下几个原因。

① 数据库的相关配置错误，无法连接数据库

* 检查数据库的相关配置，包括pom文件中的数据库连接依赖，properties文件中的数据库配置信息（密码，用户）

②  导致这个错误的另一个原因还有可能时pom文件中的 <packaging></packaging> 标签中的内容发生改变，本次错误中的packaging标签中的内容为pom，应该为jar，出现这种错误的的原因大多是因为新建一个模块之后。





在配置oss中可能也会出现上述问题，因为在oss模块中不需要加载数据库。解决方法如下：

* 添加数据库配置
* 在启动类上添加属性，默认不去加载数据库配置。
