---
date: 2020-08-18
categories: Hexo
---

# 一、github.io不能访问

1. 在浏览器中输入一个需要登录的网址时，系统会首先自动从Hosts文件中寻找对应的IP地址，一旦找到，系统会立即打开对应网页，如果没有找到，则系统再会将网址提交 DNS域名解析服务器进行该网址的IP地址解析

   * DNS域名解析服务器进行该网址的IP地址解析过程
   
   ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/27.png)

2. 不能访问的原因：电信运营商的DNS污染

3. 解决办法

   1. 修改host文件即修改域名-IP地址的关联

   2. 具体步骤

      1. 在[Dns检测|Dns查询 - 站长工具](https://tool.chinaz.com/dns/)中输入rainbow0526.github.io，查询DNS所在地及网站IP地址

         ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/34.png)

      2. 打开C:\Windows\System32\drivers\etc\hosts文件，保存网址与IP地址的关联

         ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/28.png)

# 二、修改域名

## 1、添加CNAME记录

* CNAME记录作用：把域名解析到另外一个域名

* 在生成网页的分支上新建文件CNAME，内容为rainbow0526.cn

  ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/29.png)

  文件内是这样子的：

  ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/30.png)

## 2、GitHub Pages设置Custom domain

* Github Pages 提供自定义域名：GitHub Pages supports using custom domains, or changing the root of your site's URL from the default
* 具体设置：在Custom domian中填入rainbow0526.cn

![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/31.png)

## 3、自定义域名添加解析

1. cmd命令行中`ping rainbow0526.github.io`，得到网站IP地址

   ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/32.png)

2. 到域名解析中添加解析

   ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_08/33.png)

------

*到此为止，自定义域名就修改成功啦~★,°:.☆(￣▽￣)/$:.°★ 。*

