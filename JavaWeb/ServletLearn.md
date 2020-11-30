```java
/**
 * service方法专门用来处理请求和响应。
 * Servlet接口实现
 */
@Override
public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
	System.out.println("Hello Servlet 被访问了。");
}        

//分发处理
//向下转型从而能使用getMethod方法
HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
//获取方法String
String method = httpServletRequest.getMethod();
//分发操作
if("GET".equals(method)){
	System.out.println(method);
}else if("POST".equals(method)){
	System.out.println(method);
}

//通过继承方式实现Servlet程序
//throws异常没加进去
public class HelloServlet implements HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp){
		super.doGet(req, resp);
	}

	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp){
		super.doPost(req, resp);
	}
}

//获取ServletConfig对象
getServletConfig()
//获取ServletContext对象
ServletContext servletContext= getServletConfig().getServletContext();
//获取context-parameter
servletContext.getInitParameter("username");
//获取当前工程路径
servletContext.getContextPath();
//获取当前工程物理上的绝对路径
servletContext.getRealPath("/");

//HttpServletRequest类对象的常用方法
//HttpServletRequest req
//获取请求的统一资源路径
req.getRequestURI();
//获取请求的统一资源定位符
req.getRequestURL();
//获取客户端IP
req.getRemoteHost();
//获取请求头
req.getHeader(String key);
//获取参数
req.getParameter(String name);
req.getParameterValues(String name);
//设置字符集，注意这个设置要在最开始的地方使用
req.setCharacterEncoding("UTF-8");
```
**请求转发的操作流程**
```java
//对于Servlet1而言
String username = req.getParameter("username");
username.sout;
//设置域参数
request.setAttribute("key1","value1");
//获取转发路径并转发
RequestDispatcher requestDispatcher = request.getRequestDispatcher("/contextServlet2");
requestDispatcher.forward(request,response);
//对于Servlet2而言
//便可以获得request和response的信息，同时也可以获得域参数的信息。
```
**往客户端回传数据**
```java
//会同时设置服务器和客户端都使用UTF-8字符集，还设置了响应头。
//此方法需要在获取流之前使用。
response.setContentType("text/html; charset=UTF-8");
//获取流
PrintWriter print = response.getWriter();
writer.write("response content.");
```
**请求重定向方法**
```java
//第一种方法
response.setStatus(302);
response.setHeader("Location", "http://localhost:8080");
//第二种方法（推荐使用）
response.sendRedirect("http://localhost:8080")；
```
***
```html
<head>
	<base href="http://localhost:8080/01_web/a/b/">
</head>
<body>
    <form action="http://localhost:8080/01_web/hello" method="get">
        用户名：<input type="text" name="username"><br/>
        密码：<input type="password" name="password"><br/>
        兴趣爱好：<input type="checkbox" name="hobby" value="java">Java<br/>
        <input type="submit">
        <a href="a/b/c.html">超链接</a>
    </form>
</body>
```
***
```xml
<!-- servlet标签给Tomcat服务器配置Servlet程序 -->
<servlet>
	<!-- 程序别名 -->
	<servlet-name>HelloServlet</servlet-name>
	<!-- 程序全类名 -->
	<servlet-class>com.chenzk.learn.HelloServlet</servlet-class>

	<!-- 初始化参数 -->
	<init-param>
		<param-name>username</param-name>
		<param-value>root</param-value>
	</init-param>
</servlet>

<!-- servlet-mapping标签给servlet程序配置访问地址 -->
<servlet-mapping>
	<!-- 作用：告诉服务器，我当前配置的地址给哪一个Servlet程序使用 -->
	<servlet-name>HelloServlet</servlet-name>
	<!--
    		/ 斜杠在服务器解析时，表示地址为 http://ip:port/工程路径 <br/>
    		/hello 表示地址为 http://ip:port/工程路径/hello        <br/>
 	-->
	<url-pattern>/hello</url-pattern>
</servlet-mapping>    
```

