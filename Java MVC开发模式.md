# Java MVC开发模式 #
一、MVC模式简单介绍

所谓MVC，即Model-View-Controller。

* M-->model--->模型层-->entity/dao/service

* V--> view -->视图层-->jsp/html …

* C-->controller-->控制器-->servlet

>Model层：Model指模型部分，一般在应用中Model层包括业务处理层和数据访问层。 数据访问层主要是对数据库的一些操作的封装。业务处理层应用JavaBean构建， JavaBean主要 是用作将从View层获取的数据和数据库的数据进行桥接。

>Controller层：Controller指控制部分，一般是对View层提交的请求为其设置对应的Servlet进行特定功能的处 理，这里的进行特定功能的处理一般是编写在Model中的业务处理层中的。Controller一般只是在 Web应用中充当一个中介者的作用。

>View层：View指视图部分，这一部分的内容是展示给用户实际进行交互的，通常使用JSP和HTML进行构建.

````
        请求
Client ----> controller{Servlet ----> Service ----> Dao}
  ^             |   |
  |         Model   View
  |_________________|
          响应
````
