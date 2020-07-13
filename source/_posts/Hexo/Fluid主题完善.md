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

~~~
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

~~~
<span class="label label-primary">我是行内的小小标签   OAO</span>
~~~

~~~
可选 Label：
primary default info success warning danger
~~~

* 可选便签

<span class="label label-primary">primary </span>  <span class="label label-default ">default</span>    <span class="label label-info ">info </span>  <span class="label label-success ">success </span>  <span class="label label-warning ">warning  </span> <span class="label label-danger">danger</span>

## 3、勾选框

* 样式

{% cb 我被勾选了 OwO, true, true %}

* 代码

~~~
{% cb text, checked?, incline? %}
~~~

~~~
内容解释：
text：显示的文字
checked：默认是否已勾选，默认 false
incline: 是否内联（可以理解为后面的文字是否换行），默认 false
~~~

## 4、按钮

* 样式

<a class="btn" href="https://rainbow0526.github.io/" title="卡哇伊yiyyiyi~">点我可以前往博客首页~    / 3 /</a>

* 代码格式

~~~
<a class="btn" href="https://rainbow0526.github.io/" title="卡哇伊yiyyiyi~">点我可以前往博客首页~    / 3 /</a>
~~~

# 二、首页

## 1、隐藏文章

文章开头[Front-matter](https://hexo.io/zh-cn/docs/front-matter) 中配置 `hide: true` 属性

## 2、文章摘要

 [Front-matter](https://hexo.io/zh-cn/docs/front-matter) 里设置 `excerpt：摘要文字  ` 属性

