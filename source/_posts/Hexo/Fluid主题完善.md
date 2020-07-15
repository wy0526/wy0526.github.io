---
date: 2020-07-13
categories: Hexo
---

<a class="btn" href="https://hexo.fluid-dev.com/docs/guide/#tag-插件" title="点我跳转啦/3/~">前往Tag插件文档</a>

# 一、Tag插件

## 1、便签

* 样式

<p class="note note-secondary"> 我是标签 QWQ </p>

* 代码

~~~html
<p class="note note-secondary"> 我是标签 QWQ </p>
~~~

* 可选便签

<p class="note note-primary"> primary </p>

<p class="note note-secondary"> secondary </p>

<p class="note note-success"> success </p>

<p class="note note-danger"> danger </p>

<p class="note note-warning"> warning </p>

<p class="note note-info"> info </p>

<p class="note note-light"> light </p>

## 2、行内标签

* 样式

<span class="label label-primary">我是行内的小小标签   OAO</span>

* 代码

~~~html
<span class="label label-primary">我是行内的小小标签   OAO</span>
~~~

`可选 Label：
primary default info success warning danger`

* 可选便签

<span class="label label-primary">primary </span>  <span class="label label-default ">default</span>    <span class="label label-info ">info </span>  <span class="label label-success ">success </span>  <span class="label label-warning ">warning  </span> <span class="label label-danger">danger</span>

## 3、勾选框

* 样式

{% cb 我被勾选了 OwO, true, true %}

* 代码

~~~html
{% cb text, checked?, incline? %}
~~~

内容解释：

* text：显示的文字
* checked：默认是否已勾选，默认 false
* incline: 是否内联（可以理解为后面的文字是否换行），默认 false

## 4、按钮

* 样式

<a class="btn" href="https://rainbow0526.github.io/" title="卡哇伊yiyyiyi~">点我可以前往博客首页~    / 3 /</a>

* 代码格式

~~~html
<a class="btn" href="https://rainbow0526.github.io/" title="卡哇伊yiyyiyi~">前往博客首页</a>
~~~

# 二、文章摘要

 [Front-matter](https://hexo.io/zh-cn/docs/front-matter) 里设置 

~~~shell
 excerpt：摘要文字 
~~~

# 三、加速加载

## 1、github图片

使用jsDelivr服务

使用方法（文件的绝对地址）

```text
https://cdn.jsdelivr.net/gh/user/repo@version/file
```

相关实例（博客仓库下 master 分支里 favicon 图片文件）

```text
https://cdn.jsdelivr.net/gh/fluid-dev/hexo-theme-fluid@master/source/img/favicon.png
```

## 2、加快网页加载

- 对于所有用户，将各种第三方库配置公共 CDN 是最有效的方式，可以通过配置 `_static_prefix.yml` 来链接（默认已经使用 staticfile CDN，国内用户可不做改动）；
- 如果你的域名已备案，可以使用[七牛云](https://portal.qiniu.com/signup?code=1hlwhx3ztjz2q)、阿里云、腾讯云等大厂的 OSS 服务并绑定域名，将生成后的 public 目录下全部上传到 OSS，然后你不仅可以无服务器部署博客，加载速度也将无可比拟；
- 没有备案，也可以通过香港及海外地区的云，或者私有 CDN 等方式进行加速，推荐一份 [CDN 使用指南](https://www.julydate.com/post/60859300)。
- 如果图片是存在 source 目录中，建议搭配 [hexo-all-minifier](https://github.com/chenzhutian/hexo-all-minifier) 插件，可自动对图片进行压缩；
- 如果是存放在外部的图片，建议先使用 [tinypng](https://tinypng.com/) 进行压缩。

# 四、已实现插件

## 1、密码

 [Front-matter](https://hexo.io/zh-cn/docs/front-matter) 里设置 

~~~shell
password: 131912
~~~

## 2、置顶

 [Front-matter](https://hexo.io/zh-cn/docs/front-matter) 里设置 

~~~shell
top: True
~~~

