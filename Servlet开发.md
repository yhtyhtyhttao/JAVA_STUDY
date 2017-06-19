## Servlet开发 ##
#### Servlet的部署 ####
* 由于客户端是通过URL地址访问web服务器中的资源，所以Servlet程序若想被外界访问，必须把servlet程序映射到一个URL地址上，这个工作在web.xml文件中使用<servlet>元素和<servlet-mapping>元素完成。
* <servlet>元素用于注册Servlet，它包含有两个主要的子元素：<servlet-name>和<servlet-class>，分别用于设置Servlet的注册名称和Servlet的完整类名。
* 一个<servlet-mapping>元素用于映射一个已注册的Servlet的一个对外访问路径，它包含有两个子元素：<servlet-name>和<url-pattern>，分别用于指定Servlet的注册名称和Servlet的对外访问路径。例如：

````java
<web-app>
	<servlet>
		<servlet-name>AnyName</servlet-name>
		<servlet-class>HelloServlet</servlet-class>
	</servlet>
	<servlet-mapping>
		<servlet-name>AnyName</servlet-name>
		<url-pattern>/demo/hello.html</url-pattern>
	</servlet-mapping>
</web-app>

````

#### Servlet的部署 ####
* 同一个Servlet可以被映射到多个URL上，即多个<servlet-mapping>元素的<servlet-name>子元素的设置值可以是同一个Servlet的注册名。
* 在Servlet映射到的URL中也可以使用*通配符，但是只能有两种固定的格式：一种格式是“*.扩展名”，另一种格式是以正斜杠（/）开头并以“/*”结尾。

````
<servlet-mapping>
	<servlet-name>
		AnyName
	</servlet-name>
	<url-pattern>
		*.do
	</url-pattern>
</servlet-mapping>

<servlet-mapping>
	<servlet-name>
		AnyName
	</servlet-name>
	<url-pattern>
		/action/*
	</url-pattern>
</servlet-mapping>

````

#### Servlet的部署 ####

对于如下的一些映射关系：
* Servlet1 映射到 /abc/*
* Servlet2 映射到 /*
* Servlet3 映射到 /abc
* Servlet4 映射到 *.do

问题：
* 当请求URL为“/abc/a.html”，“/abc/*”和“/*”都匹配，哪个servlet响应
	Servlet引擎将调用Servlet1。
* 当请求URL为“/abc”时，“/abc/*”和“/abc”都匹配，哪个servlet响应
	Servlet引擎将调用Servlet3。
* 当请求URL为“/abc/a.do”时，“/abc/*”和“*.do”都匹配，哪个servlet响应
	Servlet引擎将调用Servlet1。
* 当请求URL为“/a.do”时，“/*”和“*.do”都匹配，哪个servlet响应
	Servlet引擎将调用Servlet2。
* 当请求URL为“/xxx/yyy/a.do”时，“/*”和“*.do”都匹配，哪个servlet响应
	Servlet引擎将调用Servlet2。

#### Servlet接口实现类 ####

* Servlet接口SUN公司定义了两个默认实现类，分别为：GenericServlet、HttpServlet。
* HttpServlet指能够处理HTTP请求的servlet，它在原有Servlet接口上添加了一些与HTTP协议处理方法，它比Servlet接口的功能更为强大。因此开发人员在编写Servlet时，通常应继承这个类，而避免直接去实现Servlet接口。
* HttpServlet在实现Servlet接口时，覆写了service方法，该方法体内的代码会自动判断用户的请求方式，如为GET请求，则调用HttpServlet的doGet方法，如为Post请求，则调用doPost方法。因此，开发人员在编写Servlet时，通常只需要覆写doGet或doPost方法，而不要去覆写service方法。

#### web服务器调用Servlet的过程 ####
* Servlet程序是由WEB服务器调用，web服务器收到客户端的Servlet访问请求后：
 * Web服务器首先检查是否已经装载并创建了该Servlet的实例对象。如果是，则直接执行第④步，否则，执行第②步。
 * 装载并创建该Servlet的一个实例对象。
 * 创建一个用于封装HTTP请求消息的HttpServletRequest对象和一个代表HTTP响应消息的HttpServletResponse对象，然后调用Servlet的service()方法并将请求和响应对象作为参数传递进去。
 * WEB应用程序被停止或重新启动之前，Servlet引擎将卸载Servlet，并在卸载之前调用Servlet的destroy()方法。

 ![Alt text](001/Servlet生命周期.jpg "Servlet生命周期")

#### Servlet其它细节 ####
* Servlet是一个供其他Java程序（Servlet引擎）调用的Java类，它不能独立运行，它的运行完全由Servlet引擎来控制和调度。
* 针对客户端的多次Servlet请求，通常情况下，服务器只会创建一个Servlet实例对象，也就是说Servlet实例对象一旦创建，它就会驻留在内存中，为后续的其它请求服务，直至web容器退出，servlet实例对象才会销毁。
* 在Servlet的整个生命周期内，Servlet的init方法只被调用一次。而对一个Servlet的每次访问请求都导致Servlet引擎调用一次servlet的service方法。对于每次访问请求，Servlet引擎都会创建一个新的HttpServletRequest请求对象和一个新的HttpServletResponse响应对象，然后将这两个对象作为参数传递给它调用的Servlet的service()方法，service方法再根据请求方式分别调用doXXX方法。
* 如果在<servlet>元素中配置了一个<load-on-startup>元素，那么WEB应用程序在启动时，就会装载并创建Servlet的实例对象、以及调用Servlet实例对象的init()方法。

````java
举例：
	<servlet>
		<servlet-name>invoker</servlet-name>
		<servlet-class>
			org.apache.catalina.servlets.InvokerServlet
		</servlet-class>
		<load-on-startup>2</load-on-startup>
	</servlet>

````
* 用途：如果WEB应用启动时就需要启动某个框架程序，那么可以把框架程序的启动代码放到一个Servlet的init方法中，并为这个Servlet配置</load-on-startup>。这样的话，当WEB应用启动时，框架也将随之启动.

#### Servlet的线程安全问题 ####
>* 如果某个Servlet实现了SingleThreadModel接口，那么Servlet引擎将以单线程模式来调用其service方法。
>* SingleThreadModel接口中没有定义任何方法，只要在Servlet类的定义中增加实现SingleThreadModel接口的声明即可。
>* 对于实现了SingleThreadModel接口的Servlet，Servlet引擎仍然支持对该Servlet的多线程并发访问，其采用的方式是产生多个Servlet实例对象，并发的每个线程分别调用一个独立的Servlet实例对象。
>* 实现SingleThreadModel接口并不能真正解决Servlet的线程安全问题，因为Servlet引擎会创建多个Servlet实例对象，而真正意义上解决多线程安全问题是指一个Servlet实例对象被多个线程同时调用的问题。事实上，在Servlet API 2.4中，已经将SingleThreadModel标记为Deprecated（过时的）。

#### ServletConfig对象 ####
* 在Servlet的配置文件中，可以使用一个或多个<init-param>标签为servlet配置一些初始化参数。
* 当servlet配置了初始化参数后，web容器在创建servlet实例对象时，会自动将这些初始化参数封装到ServletConfig对象中，并在调用servlet的init方法时，将ServletConfig对象传递给servlet。进而，程序员通过ServletConfig对象就可以得到当前servlet的初始化参数信息。

#### ServletContext ####
* WEB容器在启动时，它会为每个WEB应用程序都创建一个对应的ServletContext对象，它代表当前web应用。
* ServletContext对象被包含在ServletConfig对象中，开发人员在编写servlet时，可以通过ServletConfig.getServletContext方法获得对ServletContext对象的引用。
* 由于一个WEB应用中
的所有Servlet共享同一个ServletContext对象，因此Servlet对象之间可以通过ServletContext对象来实现通讯。ServletContext对象通常也被称之为context域对象。

#### ServletContext应用 ####
* 多个Servlet通过ServletContext对象实现数据共享。
* 获取WEB应用的初始化参数。
* 实现Servlet的转发。
