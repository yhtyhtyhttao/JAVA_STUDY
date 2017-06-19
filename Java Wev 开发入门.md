## Java Wev 开发入门 ##

#### WEB开发的相关知识 ####

* WEB，在英语中web即表示网页的意思，它用于表示Internet主机上供外界访问的资源。

* Internet上供外界访问的Web资源分为：
 * 静态web资源（如html 页面）：指web页面中供人们浏览的数据始终是不变。
动态web资源：
 * 指web页面中供人们浏览的数据是由程序产生的，不同时间点访问web页面看到的内容各不相同。
* 静态web资源开发技术
 * Html

* 常用动态web资源开发技术：

 * JSP/Servlet、ASP、PHP等

WEB服务器

学习web开发，需要先安装一台web服务器，然后再在web服务器中开发相应的web资源，供用户使用浏览器访问。

* 常见WEB服务器
 * WebLogic
 * WebSphere
 * Tomcat

#### Servlet简介 ####
* Servlet是sun公司提供的一门用于开发动态web资源的技术。
* Sun公司在其API中提供了一个servlet接口，用户若想使用Java程序开发一个动态web资源，只需编写一个servlet接口的实现类，并把这个类部署到web服务器中，就算开发好了一个动态web资源。
* 按照一种约定俗成的称呼习惯，通常我们也把实现了servlet接口的java程序，称之为Servlet。

#### WEB应用程序 ####
* WEB应用程序指供浏览器访问的程序，通常也简称为web应用。

* 一个web应用由多个静态web资源和动态web资源组成，如:
 * html、css、js文件
 * Jsp文件、java程序、支持jar包、
 * 配置文件
 * …………

#### WEB应用的组成结构 ####
* 开发web应用时，不同类型的文件有严格的存放规则，否则不仅可能会使web应用无法访问，还会导致web服务器启动报错。

````
mail
  |
  |----html,jsp,js,css 文件等
  |
  |
  |----WEB-INF 目录
        |
        |----classes 目录-----（java类）
        |
        |
        |----lib 目录-----（java类运行所用的jar包）
        |
        |
        |web.xml 文件----（web应用的配置文件）
 ````
 * web应用中，web.xml文件是其中最重要的一个文件，它用于对web应用中的web资源进行配置。

#### web.xml文件 ####
* 通过web.xml文件，可以将web应用中的：
 * 某个web资源配置为网站首页
 * 将servlet程序映射到某个url地址上
 * …………

><font color="yellow">注意：</font>Web.xml文件必须放在web应用\WEB-INF目录下。
