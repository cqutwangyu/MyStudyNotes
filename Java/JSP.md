# JSP9个内置对象

作用： 
1、pageContext 表示页容器 EL表达式、 标签 、上传 
2、request 服务器端取得客户端的信息：头信息 、Cookie 、请求参数 ，最大用处在MVC设计模式上 
3、response 服务器端回应客户端信息：Cookie、重定向 
4、session 表示每一个用户，用于登录验证上 
5、application 表示整个服务器 
6、config 取得初始化参数，初始化参数在web.xml文件中配置 
7、exception 表示的是错误页的处理操作 
8、page 如同this一样，代表整个jsp页面自身 
9、out 输出 ，但是尽量使用表达式输出

pageContext javax.servlet.jsp.PageContext
request javax.servlet.http.HttpServletRequest 
response javax.servlet.http.HttpServletResponse 
session javax.servlet.http.HttpSession 
application javax.servlet.ServletContext 
config javax.serlvet.ServletConfig 
exception java.lang.Throwable
page java.lang.Object 
out javax.servlet.jsp.JspWriter 

**一、什么是内置对象**
在jsp开发中会频繁使用到一些对象,如ServletContext HttpSession PageContext等.如果每次我们在jsp页面中需要使用这些对象都要自己亲自动手创建就会特别的繁琐.SUN公司因此在设计jsp时,在jsp页面加载完毕之后自动帮开发者创建好了这些对象,开发者只需要使用相应的对象调用相应的方法即可.这些系统创建好的对象就叫做内置对象.

在servlet程序中,如果开发者希望使用session对象,必须通过request.getSession()来得到session对象;而在jsp程序中,开发中可直接使用session(系统帮我们创建好的session对象的名字就叫session)调用相应的方法即可,如:session.getId().

 

**二、九大内置对象**
内置对象名 类型
request	HttpServletRequest
response HttpServletResponse
config ServletConfig
application ServletContext
session HttpSession
exception Throwable
page Object(this)
out JspWriter
pageContext PageContext



**三、JSP中四大域对象**
分类:
ServletContext context域
HttpServletRequet request域
HttpSession session域 --前三种在学习Servlet时就能接触到
PageContext page域	--jsp学习的
域对象的作用:保存数据,获取数据,共享数据.
保存数据:
pageContext.setAttribute("内容");//默认保存到page域
pageContext.setAttribute("内容",域范围常量);//保存到指定域中
//四个域常量
PageContext.PAGE_SCOPE
PageContext.REQUEST_SCOPE
PageContext..SESSION_SCOPE
PageContext.APPLICATION_SCOPE
获取数据:
pageContext.getAttribute("内容");
pageContext.getAttribute("name",域范围常量);

//自动在四个域中搜索数据 pageContext.findAttribute("内容");//在四个域中自动搜索数据,顺序:page域->request域->session域->application域(context域)
域作用范围:
page域: 只能在当前jsp页面使用 (当前页面)
request域: 只能在同一个请求中使用 (转发)
session域: 只能在同一个会话(session对象)中使用 (私有的)
context域: 只能在同一个web应用中使用 (全局的)

