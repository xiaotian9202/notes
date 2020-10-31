## servlet

### 概述

web容器（container）是servlet/jsp唯一认得的HTTP服务器，servlet的执行依赖于web容器所提供的服务，没有容器，servlet只是单纯一个java类，不能称为可以提供服务的servlet。对每个请求，容器回创建一个线程并转发给适当的servlet来处理，因而可以大幅减轻性能上的负担，但也要注意线程安全问题。

### servlet示例

```java
import java.io.IOException；
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@webServlet("/hello.view")
public class HelloServletRequest extends HttpServlet {
  @override
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException,IOException {
    // 设置响应内容类型器
    response.setContentType("text/html;charset=UTF-8");
    // 取得响应输出对象
    PrintWriter out = response.getWriter();
    // 取得请求参数
    String name = request.getParameter("name");
    
    out.println("<html>");
    out.println("<head>");
    out.println("<title>Hello Servlet</title>");
    out.println("</head>");
    out.println("<body>");
    out.println("<h1>Hello" + name + "!<h1>");
    out.println("</body>");
    out.println("</html>");
    
    out.close();
  }
}

```

如果请求的URL是hello.view，就会由HelloServlet来处理，容器接收到客户端的HTTP请求后，会收集HTTP请求中的信息，并分别创建代表请求和响应的java对象，并在调用doGet()方法时将这两个对象当作参数传入。

当请求来到时，容器会调用Servlet的service()方法，但是service方法是在Servlet的子类HttpServlet中实现的，实现代码如下：

```java
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOExcption {
  // 取得请求的方法
  String method = req.getMethod();
  if （method.equals(METHOD_GET)) {
    // ...
    doGet(req, resp);
    // ...
  } else if (method.equals(METHOD_HEAD)) {
    // ...
    doHead(req, resp);
  } else if (method.equals(METHOD_POST)) {
    // ...
    doPost(req, resp);
  } else if (method.equals(METHOD_PUt)) {
    // ...
  }
}
```

会先判断HTTP的请求方式，在分别调用对应的方法，所以若要使用对应的方法进行处理，则需要重写对应的方法。

当应用启动时，并不会创建所有的servlet实例，而是在请求到来时，将需要的servlet类实例化，进行初始化操作，然后再处理请求，若想在应用程序启动时，就将Servlet载入、实例化并做好初始化动作，则可以使用loadOnStartup设置，设置大于0的值（默认值为-1），表示启动应用程序后就会初始化Servlet，数字代表了Servlet的初始化顺序，数字越小，越早初始化，多个数字相同，则由容器自行决定。

### 目录结构

```text
- WEB-INF
	- web.xml  web应用程序部署描述文件
	- lib  放置JAR文件的目录
	- classes  放置编译过后.class文件的目录
	
```

/WEB_INF/web.xml是部署描述文件

/WEB_INF/classes用来放置应用程序用到的自定义类(.class),必须包括包(Package)结构

/WEB-INF/lib用来放置应用程序用到的JAR文件

web应用程序用到的JAR文件，其中可以放置Servlet、JSP、自定义类、工具类、部署描述文件等，应用程序的类载入器可以从JAR中载入对应的资源。

如果要用到某个类，则web应用程序会到/WEB_INF/classes中试着载入类，若无，再试着从/WEB_INF/lib的JAR文件中寻找类文件，若还未找到，则会到容器实现本身存放类或JAR的目录中寻找。

