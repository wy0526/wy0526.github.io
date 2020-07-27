---
date: 2020-07-26
categories: MVC开发模式、el表达式、jstl标签
---

# 一、MVC开发模式

1. jsp演变历史

   1. 早期只有servlet，只能使用response输出标签数据，非常麻烦
   2. 后来又jsp，简化了Servlet的开发，如果过度使用jsp，在jsp中即写大量的java代码，有写html表，造成难于维护，难于分工协作
   3. 再后来，java的web开发，借鉴mvc开发模式，使得程序的设计更加合理性

2. MVC

   1. M：Model，模型➡JavaBean
       * 完成具体的业务操作，如：查询数据库，封装对象
   2. V：View，视图➡JSP
       * 展示数据
   3. C：Controller，控制器➡Servlet
       * 获取用户的输入
       * 调用模型
       * 将数据交给视图进行展示

3. 优缺点

   1. 优点

        1. 耦合性低，方便维护，可以利于分工协作

        2. 重用性高

   2. 缺点：

        使得项目架构变得复杂，对开发人员要求高

![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_07/33.png)

# 二、EL表达式

1. 概念：Expression Language 表达式语言

2. 作用：替换和简化jsp页面中java代码的编写

3. 语法：`${表达式}`

4. 注意：
	* jsp默认支持el表达式的。如果要忽略el表达式
		1. 设置jsp中page指令中：`isELIgnored="true"` 忽略当前jsp页面中所有的el表达式
		2. `\${表达式}` ：忽略当前这个el表达式
	
5. 使用

   1. 运算——运算符

      1. 算数运算符： +、- 、* 、/(div) 、%(mod)
      2. 比较运算符： > 、< 、>=、 <=、 ==、 !=
      3. 逻辑运算符： && (and)、 ||(or)、 !(not)
      4. 空运算符： empty
           * 功能：用于判断字符串、集合、数组对象是否为null或者长度是否为0
           * `${empty list}`：判断字符串、集合、数组对象是否 为 null或者长度为0
           * `${not empty str}`：表示判断字符串、集合、数组对象是否 不为 null 并且 长度>0

   2. 获取值

      1. el表达式只能从域对象中获取值

      2. 语法

          1. `${域名称.键名}`：从指定域中获取指定键的值

             * 域名称

               | 域名称           | 指定域                        |
               | ---------------- | ----------------------------- |
               | pageScope        | pageContext                   |
               | requestScope     | request                       |
               | sessionScope     | session                       |
               | applicationScope | application（ServletContext） |

             * 举例：在request域中存储了name=张三，通过${requestScope.name}来获取指定域request中指定键name的值

             * 如果指定的键不存在，显示的是空字符串

          2. `${键名}`：表示依次从最小的域中查找是否有该键对应的值，直到找到为止。

          3. 获取对象、List集合、Map集合的值

             1. 对象

                * `${域名称.键名.属性名}`

                * 本质上会去调用对象的getter方法

             2. List集合

                * `${域名称.键名[索引]}`
                * 索引不存在会报错

             3. Map集合

                * `${域名称.键名.key名称}`
                * `${域名称.键名["key名称"]}`

      3. 隐式对象

          * el表达式中有11个隐式对象
          * pageContext：获取jsp其他八个内置对象
            * `${pageContext.request.contextPath}`：动态获取虚拟目录

# 三、JSTL标签

1. 概念：JavaServer Pages Tag Library  JSP，标准标签库。是由Apache组织提供的开源的免费的jsp标签。

2. 作用：用于简化和替换jsp页面上的java代码

3. 使用步骤

   1. 导入jstl相关jar包
   2. 引入标签库：taglib指令` <%@ taglib %>`
   3. 使用标签

4. 常用的JSTL标签

   1. if：相当于java代码的if语句

      1. 属性

         test为必须属性，接收boolean表达式

         * 如果表达式为true，则显示if标签体内容，如果为false，则不显示标签体内容
         * 一般情况下，test属性值会结合el表达式一起使用

      2. 注意

         `<c:if></c:if>`标签没有else情况，想要else情况，则可以在定义一个`<c:if></c:if>`标签

   2. choose:相当于java代码的switch语句

      1. 使用choose标签声明，相当于switch声明
      2. 使用when标签做判断，相当于case
      3. 使用otherwise标签做其他情况的声明，相当于default

   3. foreach:相当于java代码的for语句

      1. 完成重复操作
         * 属性
           1. begin：开始值
           2. end：结束值
           3. var：临时变量
           4. step：步长
           5. varStaus：循环状态对象（多数在遍历容器时使用）
              * index：容器中元素的索引，从0开始
              * count：循环次数，从1开始
      2. 遍历容器
         * 属性
           1. items：容器对象
           2. var：容器中元素的临时变量
           3. varStaus：循环状态对象（多数在遍历容器时使用）
              * index：容器中元素的索引，从0开始
              * count：循环次数，从1开始

5. 练习

   * 需求：在request域中有一个存有User对象的List集合。需要使用jstl+el将list集合数据展示到jsp页面的表格table中

# 四、三层架构

软件设计架构

1. 界面层（表示层）：用户看的界面。用户可以通过界面上的组件和服务器进行交互
2. 业务逻辑层：处理业务逻辑的。登录、注册等，最终为了访问数据库
3. 数据访问层：操作数据存储文件

![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_07/35.png)

接下来学习的框架其实是对上述三层的简化。

ssm：SpringMVC框架、MyBatis框架、Spring框架（javaee灵魂框架）

# 五、案例:用户信息列表展示

