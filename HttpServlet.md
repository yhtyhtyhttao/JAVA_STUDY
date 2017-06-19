# HttpServlet #

### HttpServletRequest ###

* HttpServletRequest对象代表客户端的请求，当客户端通过HTTP协议访问服务器时，HTTP请求头中的所有信息都封装在这个对象中，开发人员通过这个对象的方法，可以获得客户这些信息。

#### Request常用方法 ####
* 获得客户机信息
 * getRequestURL方法返回客户端发出请求时的完整URL。
 * getRequestURI方法返回请求行中的资源名部分。
 * getQueryString 方法返回请求行中的参数部分。
 * getPathInfo方法返回请求URL中的额外路径信息。额外路径信息是请求URL中的位于Servlet的路径之后和查询参数之前的内容，它以“/”开头。
 * getRemoteAddr方法返回发出请求的客户机的IP地址
 * getRemoteHost方法返回发出请求的客户机的完整主机名

#### HTTP响应 ####
* 一个HTTP响应代表服务器向客户端回送的数据，它包括：
 * 一个状态行、若干响应头、以及实体内容 ，其中的一些消息头和实体内容都是可选的，消息头和实体内容之间要用空行隔开。
* 例：

````
HTTP/1.1 200 OK                  <--------------- 状态行
Server: Microsoft-IIS/5.0        -------------|
Date: Thu, 13 Jul 2000 05:46:53 GMT           |
Content-Length: 2291                          |--- 多个消息头
Content-Type: text/html                       |
Cache-control: private           -------------|
                                 <--------------- 一个空行
<HTML>                           <------------|
<BODY>                           <------------|--- 实体内容
…………
````

#### HTTP响应的细节——状态行 ####
* 状态行
 * 格式： HTTP版本号　状态码　原因叙述<CRLF>
 * 举例：HTTP/1.1 200 OK
* 状态码用于表示服务器对请求的处理结果，它是一个三位的十进制数。响应状态码分为5类，如下所示：
 * 100~199       表示成功接收请求，要求客户端继续提交下一次请求才能完成整个处理过程
 * 200~299       表示成功接收请求并已完成整个处理过程，常用200
 * 300～399      为完成请求，客户需进一步细化请求。例如，请求的资源已经移动一个新地址，常用302、307和304
 * 400～499      客户端的请求有错误，常用404
 * 500～599      服务器端出现错误，常用 500

### HttpServletResponse ###

Web服务器收到客户端的http请求，会针对每一次请求，分别创建一个用于代表请求的request对象、和代表响应的response对象。

request和response对象即然代表请求和响应，那我们要获取客户机提交过来的数据，只需要找request对象就行了。要向客户机输出数据，只需要找response对象就行了。

* HttpServletResponse对象服务器的响应。这个对象中封装了向客户端发送数据、发送响应头，发送响应状态码的方法。

#### response细节 ####
* getOutputStream和getWriter方法分别用于得到输出二进制数据、输出文本数据的ServletOuputStream、Printwriter对象。
* getOutputStream和getWriter这两个方法互相排斥，调用了其中的任何一个方法后，就不能再调用另一方法。
* Servlet程序向ServletOutputStream或PrintWriter对象中写入的数据将被Servlet引擎从response里面获取，Servlet引擎将这些数据当作响应消息的正文，然后再与响应状态行和各响应头组合后输出到客户端。
* Serlvet的service方法结束后，Servlet引擎将检查getWriter或getOutputStream方法返回的输出流对象是否已经调用过close方法，如果没有，Servlet引擎将调用close方法关闭该输出流对象。
