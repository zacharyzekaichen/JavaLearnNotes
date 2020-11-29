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
```

```html
<body>
    <form action="http://localhost:8080/01_web/hello" method="get">
        <input type="submit">
    </form>
</body>
```

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

