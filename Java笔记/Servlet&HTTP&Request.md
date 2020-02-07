# 今日内容
	1. Servlet
	2. HTTP协议
	3. Request


## Servlet
	1. 概念
	2. 步骤
	3. 执行原理
	4. 生命周期
	5. Servlet3.0 注解配置
	6. Servlet的体系结构
		Servlet --接口
			|
		GenericServlet --抽象类
			|
		HttpServlet --抽象类

		* GenericServlet : 将Servlet接口中其它方法做了默认空实现,只将Service方法做了抽象
			*将来定义Servlet类时,可以继承 GenericServlet,实现service方法,如果需要写其他方法可以继续复写

		* HttpServlet : 对http协议的一种封装,简化操作
			1. 定义类继承HttpServlet
			2. 复写doGet/dopost方法
	7. Servlet相关配置
		1. urlpattern : Servlet访问路径,如果是多个路径用"{}"将其引起来
			1. 一个Servlet可以定义多个访问路径 
			2. 路径定义规则
				1. /xxx : 路径匹配
				2. /xxx/xxx : 多重路径 : 目录结构
				3. *.do :扩展名匹配
## HTTP : 
	* 概念 : Hyper Text Transfer Protocol 超文本传输协议
		* 传输协议 : 定义了,客户端和服务器端通信时,发送数据的格式
		* 特点 :
			 1. 基于TCP/IP的高级协议
			 2. 默认端口号: 80
				 https://www.baidu.com:80
			 3. 基于请求/响应模型的:一次请求对应一次响应
			 4. 无状态的 : 每次请求之间相互独立,不能交互数据
			 
		* 历史版本 :
			*  1.0 : 每一次请求响应都会建立新的连接
			*  1.1 : 复用连接 : 在传输之后会有等待时间如果后续有数据需要传输则继续使用这个连接

	* 请求消息数据格式
		1. 请求行
			格式 : 请求方式 请求url 请求协议/版本
					GET /login.html HTTP/1.1
			* 请求方式
				* HTTP协议中有7种请求方式,常用的有两种
					* GET :
						1. 请求参数在请求行中,在url后
						2. 请求的url长度有限制
						3. 不太安全
					* POST :
						1. 请求的参数在请求体中
						2. 请求的url长度没有限制
						3. 相对安全
		2. 请求头 : 客户端浏览器告诉服务器一些信息
			请求头名称 : 请求头值
			* 常见的请求头
				1. User-Agent : 浏览器告诉服务器,我访问你使用的浏览器版本信息
					* 可以在服务器端获取该头的信息,解决浏览器的兼容问题	

				2. Referer : http : //localhost/login.html
					* 告诉服务器,我(当前请求)从哪里来?
						* 作用 :
							1. 防盗链
							2. 统计工作
		3. 请求空行
			空行, 就是用于分割POST请求头和请求体的
		4. 请求体(正文) :
			* 封装POST请求消息的请求参数的
	* 响应消息数据格式



## Request :
	1. request 和 response 对象的原理
		1.  request 和 response对象是由Tomcat服务器创建的,我们来使用它们
		2.   request 对象是来获取请求消息, response对象是用来设置响应消息的

			1. 客户端浏览器提交数据通过url地址访问服务器
			2. 服务器会根据请求url中的资源路径,创建对应的Servlet对象
			3. 服务器会创建request 和 response 对象, request对象中封装请求消息数据
			4. 服务器会将request 和 response 对象, 传递给service方法,并调用service方法
			5. 程序员在service方法设置响应消息
			6. 服务器在给浏览器做出响应之前会从response对象中拿程序员设置的响应消息数据

	2.request的继承体系结构
		ServletRequest  -- 接口
			|	继承
		HttpServlete  -- 接口
			|	实现
		org.apache.catalina.connector.RequestFacade@4b4cf641
	3.request 功能
		1. 获取请求消息数据
			1. 获取请求行
				*  GET /day_28/demo02?name=zhangsan HTTP/1.1
				*  方法:
					1.  获取请求方式 : GET
						* String getMethod();
					2. (*)获取虚拟目录 : /day_28
						* String getContextPath()
					3. 获取Servlet路径 : /demo02
						* String getServletPath()
					4. 获取get方式请求参数 : name=zhangsan
						* String getQuerystring()
					5. (*)获取请求URI : /day_28/demo02
						* String getRequestURI() :  /day_28/demo02
						* StringBuffer getRequestURL() : http://localhost/day_28/demo02

						* URL : 统一资源定位符 : http://localhost/day_28/demo02
						* URI : 统一资源标识符  : /day_28/demo02
					6. 获取协议及版本信息 : HTTP/1.1
						* String getProtocol()
					7. 获取客户机的IP地址
						* String getRemoteAddr()
			2. 获取请求头
			3. 获取请求体
		2. 
