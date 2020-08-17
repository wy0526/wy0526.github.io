---
date: 2020-08-10
categories: Maven
---

# 一、简介

## 1、Maven概述

1. Maven是一个项目的构建工具
2. Maven作用
   * 管理依赖
     1. maven可以管理jar文件
     2. 自动下载jar和他的文档，源代码
     3. 管理jar直接的依赖，a. jar需要b.jar，maven会自动下载b. jar
     4. 管理你需要的jar版本
     5. 编译程序，把java编译为class
     6. 测试你的代码是否正确
     7. 打包文件，形成jar文件， 或者war文件
     8. 部署项目
   * 构建项目
     * 构建是面向过程的，就是一些步骤，完成项目代码的编译，测试，运行，打包，部署等等
     * maven支持的构建包括有
       1. 清理。把之前项目编译的东西删除掉，为新的编译代码做准备
       2. 编译。把程序源代码编译为执行代码，java-class文件
          批量的，maven可 以同时把成千上百的文件编译为class.
          javac不-一样，javac一次编译一个文件
       3. 测试。maven可 以执行测试程序代码，验证你的功能是否正确。
          测试是批量的，maven同时执行多个测试代码，同时测试很多功能.
       4. 报告。生成测试结果的文件，测试通过没有
       5. 打包。把你的项目中所有的class文件，配置文件等所有资源放到一个压缩文件中，这个压缩文件就是项目的结果文件。通常 java程序，压缩文件是jar扩展名的。对于web应用，压缩文件扩展名是.war
       6. 安装。 把5中生成的文件jar, war安装到本机仓库
       7. 部署。把程序安装好可以执行
3. 使用方式
   1. 独立使用maven：使用maven的各种命令，完成代码的编译，测试，打包等
   2. 结合开发工具使用：一般在idea中使用maven，简单、快捷、不需要记命令

## 2、安装

1. 从maven的官网下载maven的安装包apache- maven-3.3. 9-bin. zip

2. 解压安装包，解压到一个目录，非中文目录

   * bin：执行程序，主要是mvn. cmd
   * conf ：maven 工具本身的配置文件settings . xml

3. 配置环境变量

   1. 在系统的环境变量中，指定一个`M2_HOME`的名称，它的值是maven工具安装目录，即bin之前的目录，如：

      ~~~
      M2_HOME
      D:\ComputerSoftware\apache-maven-3.6.3
      ~~~

   2. 把M2_ HOME加入到path之中。在所有路径之前加入`%M2_HOME%\bin;`

4. 验证：cmd命令行中，执行`mvn -v`

   * 注意：需要配置`JAVA HOME`，指定jdk路径

   * 验证成功显示

     ~~~
     C:\Users\15784>mvn -v
     Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
     Maven home: D:\ComputerSoftware\apache-maven-3.6.3\bin\..
     Java version: 1.8.0_251, vendor: Oracle Corporation, 
     runtime: D:\ComputerSoftware\Java\jdk1.8.0_251\jre
     Default locale: zh_CN, platform encoding: GBK
     OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
     ~~~

# 二、核心概念

1. POM：一个文件，名称是pom.xml，pom翻译过来叫做项目对象模型。maven把一一个项目当做一个模型使用。控制maven构建项目的过程，管理jar依赖
   * 坐标：是一个唯一的字符串，用来表示资源的
   * 依赖管理：管理你的项目可以使用jar文件
2. 约定的目录结构：maven项目的目录和文件的位置都是规定的
3. 仓库管理(了解)：你的资源存放的位置
4. 生命周期(了解)：maven工具构建项目的过程，就是生命周期
5. 插件和目标(了解) ：执行maven构建的时候用的工具是插件
6. 继承
7. 聚合

## 1、约定的目录结构

每一个maven项目在磁盘中都是一个文件夹，如：项目Hello

~~~
Hello/
    ----/src
    --------/main					   #放你主程序java代码和配置文件
    -----------------/java			   #你的程序包和包中的java文件
    -----------------/resources		   #你的java程序中要使用的配置文件
    --------/test					   #放测试程序代码和文件的(可以没有)
    -----------------/java			   #测试程序包和包中的java文件
    -----------------/resources	       #测试java程序中要使用的配置文件
    ----/pom. xml					   #maven的核心文件(maven项目必须有)
~~~

## 2、仓库

1. 手动创建一个maven工程
   * 创建好工程目录后，在cmd命令行中执行命令`mvn compile`会编译src/main目录下的所有java文件。编译前会下载一些jar文件（叫做插件，插件是完成某些功能），因为maven工具执行的操作需要很多插件( java类--jar文件)完成的。下载的东西存放到了默认仓库(本机仓库) ：C: \Users\ ( 登录操作系统的用户名) Adninistrator\ . m2\repository
   * 执行`mvn compile` 结果是在项目的根目录下生成target目录(结果目录)，maven编译的java程序，最后的class文件都放在target目录中
   * 自定义本机存放资源的目录位置
     1. 修改maven的配置文件，maven安装目录/conf/settings . xml，先备份settings . xml
     2. 修改标签`<localrepositoy>`指定你的目录(不要使用中文目录)

2. 概念

   仓库是存放东西的，存放maven使用 的jar和我们项目使用的jar

   * maven使用的插件( 各种jar)
   * 我项目使用的jar(第三方的工具)

3. 分类

   * 本地仓库：就是你的个人计算机上的文件夹，存放各种jar
   * 远程仓库：在互联网上的，使用网络才能使用的仓库
     1. 中央仓库：最权威的，所有的开发人员都共享使用的一个集中的仓库,
        中央仓库的地址： [https://repo.maven.apache.org](https://repo.maven.apache.org)
     2. 中央仓库的镜像：就是中央仓库的备份，在各大洲， 重要的城市都是镜像
     3. 私服：在公司内部，在局域网中使用的，不是对外使用的

4. 使用

   * maven仓库的使用不需要人为参与，会自行进行下面的步骤
   * 开发人员需要使用mysql驱动 ---> maven首先查本地仓库 ---> 私服 ---> 镜像 ---> 中央仓库

## 3、POM文件

1. 概念

   Project Object Model项目对象模型。Maven 把一个项目的结构和内容抽象成一个模型 ，在xml文件中进行声明，以方便进行构建和描述，pom.xml是Maven的灵魂。所以，maven环境搭建好之后，所有的学习和操作都是关于pom.xml的

2. 文件内容

   1. 坐标（gav）

      唯一值， 在互联网中唯一标识一个项目

      * groupId：组织id，一般是公司域名的倒写。格式可以为:
        * 域名倒写。 例如com.baidu
        * 域名倒写+项目名。例如com.baidu.appolo
      * artifactId：项目名称，也是模块名称，对应groupId中项目中的子项目
      * version：项目的版本号。如果项目还在开发中，是不稳定版本，通常在版本后带-SNAPSHOT。version使用三位数字标识，例如1.1.0

      ~~~
      <groupId>公司域名的倒写</groupId>
      <artifactId>自定义项目名称</arti factId>
      <version>自定版本号</version>
      ~~~

   2. 打包：packaging

      项目打包的类型，可以使用jar、war、rar、ear、pom。默认是jar，web应用是war

   3. 依赖：dependencies和dependency

      * 相当于是java代码中import。例如，你的项目中要使用的各种资源说明，比我的项 目要使用mysql驱动

      ~~~
      <dependencies>
          <!--依赖java代码中 import -->
          <dependency>
              <groupId>mysq1</groupId>
              <arti factId> mysq1 -connector- java</arti factId>
              <version>5.1.9</version>
          </dependency>
      </dependencies>
      ~~~

      * 依赖范围

        scope的值有complie（默认）、test、provided，用以表示jar包等依赖的适用范围

        * complie：编译，测试，打包，部署
        * test：测试
        * provided：编译，测试

   4. 属性：properties

      * 定义一些配置属性。例如：project.build.sourceEncoding (项目构建源码编码方式)，可以设置为UTF-8， 防止中文乱码，也可定义相关构建版本号，便于日后统一 升级

      * 自定义属性

        一般用于定义依赖的版本号

        1. 在`<properties>`通过自定义标签声明变量（标签名就是变量名）
        2. 在pom.xml文件中的其他位置，使用`${标签名}`使用变量的值

   5. 构建：build

      * maven在进行项目的构建时，配置信息，例如，指定编译java代码使用的jdk版本

      * 资源插件

        1. 默认没有使用resources的时候，maven执行编译代码时，会 把src/main/resources目录中的文件拷贝到target/classes目录中。对于src/main/java 目录下的非java文件不处理，不拷贝到target/classes目录中。
        2. 如果编译时，要将src/main/java 目录下的非java文件也拷贝到target/classes目录中，则可以在`<build>`中加入`<resources>`

        ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/09.png)

## 4、生命周期

maven生命周期：maven构建项目的过程，清理，编译，测试，报告，打包，安装，部署

## 5、常用命令

maven的命令：maven独立使用时，通过命令完成maven的生命周期的执行。maven可以使用命令，完成项目的清理，编译，测试等等

1. 单元测试

   * 用的是junit，junit是一个专门测试的框架(工具) 。junit测试的是类中的方法，每一个方法都是独立测试的。maven借助单元测试，批量的测试你类中的大量方法是否符合预期的

   * 使用步骤

     1. 加入依赖，在pom. xml加入单元测试依赖

        ~~~
        <!--单元测试-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactid>
            <version>4.11</version>
            <scope>test</scope>
        </dependency>
        ~~~

     2. 在maven项目中的src/test/java目录下，创建测试程序。推荐的创建类和方法的提示：

        1. 测试类的名称是Test +你要测试的类名
        2. 测试的方法名称是:Test+方法名称

   * 举例

     例如，你要测试的类是HelloMaven，则先创建测试类TestHelloMaven

     ~~~
     @Test
     public void testAdd() {
     	测试HelloMaven的add方法是否正确
     }
     ~~~

     其中testAdd叫做测试方法，它的定义规则如下：

     1. 方法是public的，必须的
     2. 方法没有返回值，必须的
     3. 方法名称是自定义的，推荐是Test +方法名称
     4. 在方法的上面加入`@Test`

2. 常用命令

   以下命令要在pom.xml所在目录下执行

   * `mvn clean`清理
     * 作用：清理编译后的目录即target文件夹
   * `mvn complie`编译
     * 作用：只编译main目录，不编译test目录
     * 结果：.class文件存放在target/classes目录中
   * `mvn test-complie`编译
     * 作用：只编译test目录，不编译main目录
     * 结果：.class文件存放在target/test-classes目录中
   * `mvn test`测试
     * 作用：运行test目录进行测试
     * 过程：编译测试、测试
     * 结果：target/surefire-reports目录保存测试结果
   * `mvn package`打包
     * 作用：打包主程序
     * 过程：编译、编译测试、测试、打包
     * 结果：jar包（javase）或者war包（web）保存在target/***artifactId+version***  
   * `mvn install`安装
     * 作用：本地多个项目共用一个jar包
     * 过程：编译、编译测试、测试、打包、安装
     * 结果：包保存在本地仓库

## 6、插件

maven的插件：maven命令执行时，真正完成功能的是插件，插件就是一些jar文件，一些类。在pom.xml文件中进行配置

~~~
<!--build是控制配置maven构建项目的参数设置，设置jdk的版本--> .
<build>
    <!-- 配置插件-->
    <p1ugins>
        <plugin>
            <groupId>org . apache. maven. p1ugins</groupId>
            <!-- 插件的名称 -->
            <artifactId>maven- compiler-plugin< /artifactId>
            <!-- 插件的版本 -->
            <version>3.8.1</version>
            <!-- 配置插件的信息 -->
            < configuration>
                <!-- 告诉maven我们的代码实在jdk1.8上编译的 -->
                <source>1.8</source>
                <!-- 我们的程序应该运行在1.8的jdk上 -->
                <target>1.8</target>
            </ configuration>
        </plugin>
    </plugins>
</build>
~~~

# 三、在IDEA中的应用

## 1、IDEA中设置Maven

> idea中内置了maven，一 般不使用内置的，因为用内置修改maven的设置不方便
> 使用自己安装的maven，需要覆盖idea中的默认的设置，让idea指 定maven安装位置等信息

1. 当前工程配置maven

   点击菜单栏`File` --- `Settings` --- `Build, Excution , Deployment` --- `Build Tools`
    --- `Maven`，配置下面的内容：

   * Maven Home directory: maven的安装目录
   * User settings File：maven安装目录下conf/setting.xml配置文件
   * Local Repository：本机仓库的目录位置

   然后点击Maven下的`Runner`，配置下面的内容：

   * VM Options：-DarchetypeCatalog=internal
   * JRE：你项目的jdk

   > -DarchetypeCatalog=internal：
   >
   > maven项目创建时，会联网下载模版文件，比较大，使用archetypeCatalog- internal，不用下载，创建maven项目速度快

2. 新建工程配置maven

   点击菜单栏`File` --- `New Projects Settings` --- `Settings for New Projects` --- `Build, Excution , Deployment` --- `Build Tools`进行配置，配置内容和上述相同

![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/07.png)

![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/08.png)

## 2、IDEA使用模板创建项目

1. 普通的java项目

   1. 创建步骤

      File ---> new module ---> maven项目 ---> <u>maven-archetype-quickstart</u> ---> 修改项目坐标（ 如果没有提前设置idea中新建项目的maven配置，则还需要设置maven的配置）

   2. 项目结构

      ~~~
      ├─src
      │  ├─main
      │  │  ├─java
      │  │  │  └─com
      │  │  │      └─bjpowernode
      │  │  │              HelloMaven.java
      │  │  │              
      │  │  └─resources
      │  └─test
      │      ├─java
      │      │  └─com
      │      │      └─bjpowernode
      │      │              TestHelloMaven.java
      │      │              
      │      └─resources
      └─target
      ~~~

   * 在cmd窗口中执行`tree /f >目录.txt`可以将文件结构输出到本文件夹下的目录.txt中

2. web工程

   1. 创建步骤

      File ---> new module ---> maven项目 ---> <u>maven-archetype-webapp</u> ---> 修改项目坐标（ 如果没有提前设置idea中新建项目的maven配置，则还需要设置maven的配置）

   2. 项目结构

      ~~~
      ├─src
      │  ├─main
      │  │  ├─java
      │  │  │  └─com
      │  │  │      └─bjpowernode
      │  │  │          └─controller
      │  │  │                  HelloServlet.java
      │  │  │                  
      │  │  ├─resources
      │  │  └─webapp
      │  │      │  index.jsp
      │  │      │  main.jsp
      │  │      │  
      │  │      └─WEB-INF
      │  │              web.xml
      │  │              
      │  └─test
      │      ├─java
      │      └─resources
      └─target
      ~~~

