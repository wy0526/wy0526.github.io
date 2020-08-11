---
date: 2020-08-04
categories: JSON
---

# 一、概念

1. JavaScript Object Notation		JavaScript对象表示法

~~~java
//java
Person p = new Person();
p.setName("张三");
p.setAge(23);
p.setGender("男");

//JSON
var p = {"name":"张三","age":23,"gender":"男"};
~~~

* json现在多用于存储和交换文本信息的语法
* 进行数据的传输
* JSON 比 XML 更小、更快，更易解析

# 二、语法

1. 基本规则
   * 数据在名称/值对中：json数据是由键值对构成的
     * 键用引号(单双都行)引起来，也可以不使用引号
     * 值的取值类型
       1. 数字（整数或浮点数）
       2. 字符串（在双引号中）
       3. 逻辑值（true 或 false）
       4. 数组（在方括号中）如：{"persons":[{},{}]}
       5. 对象（在花括号中），如：{"address":{"province"："陕西"....}}
       6. null
2. 获取数据
   1. json对象.键名
   2. json对象["键名"]
   3. 数组对象[索引]
   4. 遍历

~~~
var person = {"name": "张三", age: 23, 'gender': true};

var ps = [{"name": "张三", "age": 23, "gender": true},
          {"name": "李四", "age": 24, "gender": true},
          {"name": "王五", "age": 25, "gender": false}];

//获取person对象中所有的键和值
//for in 循环

/* for(var key in person){
    //这样的方式获取不行。因为相当于  person."name"
    //alert(key + ":" + person.key);
    alert(key+":"+person[key]);
}*/
		
//获取ps中的所有值

for (var i = 0; i < ps.length; i++) {
	var p = ps[i];
    for(var key in p){
        alert(key+":"+p[key]);
    }
}
~~~

# 三、JSON数据和Java对象的相互转换

![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/02.png)

* JSON解析器
  * 常见的解析器：Jsonlib，Gson，fastjson，jackson

1. Java对象转换JSON

   1. 使用步骤

      1. 导入jackson的相关jar包
      2. 创建Jackson核心对象 ObjectMapper
      3. 调用ObjectMapper的相关方法进行转换

   2. 转换方法

      1. `writeValue(参数1，obj)`

         参数1： 

         * File：将obj对象转换为JSON字符串，并保存到指定的文件中
         * Writer：将obj对象转换为JSON字符串，并将json数据填充到字符输出流中
         * OutputStream：将obj对象转换为JSON字符串，并将json数据填充到字节输出流中

      2. `writeValueAsString(obj)`:将对象转为json字符串

   3. 注解

      1. `@JsonIgnore`：排除属性
      2. `@JsonFormat`：属性值的格式化
         * @JsonFormat(pattern = "yyyy-MM-dd")

   4. 复杂java对象转换

      1. List：数组
      2. Map：对象格式一致

2. JSON转为Java对象

   1. 导入jackson的相关jar包
   2. 创建Jackson核心对象 ObjectMapper
   3. 调用ObjectMapper的相关方法进行转换
      * `readValue(json字符串数据,Class)`

# 四、案例：校验用户名是否存在