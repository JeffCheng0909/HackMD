# Spring Boot Udemy

### 建立Maven新專案
1. Right-click new project > Maven Project
2. V Create a simple project 
   V Use default Workspace location
3. Fill Group Id、Artifact Id、Version(0.0.1-SNAPSHOT)、Packaging(jar)、
4. Fill Group Id(org.springframework.boot)、Artifact Id(spring-boot-starter-parent)、Version(2.4.2)
5. Project Right-click > Properties > Java Build Path > Edit JDK1.8 verison
6. Project Facets > Dynamic Web Module(4.0)、Java(1.8) and click Further configuration available > Generate web.xml
7. Project Right-click properties > Deployment Assembly > add > Java Build Path Entries > Maven Dependencies > Finish

#### dependency(引入Jar包)
```
//引入SpringMVC、Servlet、Filter、Listener等Jar包

<dependencies>
    <dependency>	
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>	
```

#### 更改Port號
點選src/main/resources/application.properties或application.yml更改port號
```
application.properites:
server.port=8081

application.yml:
server
  port: 8081
```


#### 建立Controller
>@Controller、@RestController、@RequestMapping、@ResponseBody

path:src/main/java
package:cn.sm1234.controller
```
package cn.sm1234.controller;

import java.util.HashMap;
import java.util.Map;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
//@RequestMapping("/hello")  //可上下都寫，或寫下面
public class HelloController {
	
    private Map<String,Object> result = new HashMap<String,Object>();
	
    @RequestMapping("/abc")
    @ResponseBody //轉換JSON註解
    public Map<String,Object> hello() {
        result.put("name", "eric");
        result.put("gender", "男");
        return result; //將會返回一個JSON的數據在頁面上
    }
}


@RestController  //可代替@Controller + @ResponseBody
//@Controller
public class HelloController {
	
    private Map<String,Object> result = new HashMap<String,Object>();
	
    @RequestMapping("/abc")
    //@ResponseBody
    public Map<String,Object> hello() {
        result.put("name", "eric");
        result.put("gender", "男");
        return result; //將會返回一個JSON的數據在頁面上
    }
}
```

#### RequestMapping差異
```
@RequestMapping("/demo3") //打在URL的請求

return "demo2"; //跳轉到demo2.html頁面


@RequestMapping("/hello") //打在URL的請求

return result;  //跳轉到當下空白頁面
```

#### 建立Spring Boot啟動器 
>@SpringBootApplication

path:src/main/java
package:cn.sm1234
//要放在Controller package的外面才能啟動，和Controller.java同層級會無法啟動。
```
package cn.sm1234;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {
	
	//固定寫法
	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}
}
```

### Servelt & Spring Boot 差別

```
//Spring Boot

html:
//!Action的第一步是直接找有@標註的Controller檔案
//Action後的名稱會直接用@RequestMapping(XXX)寫在Controller上方。
<form action="uploadAttach" method="post" enctype="multipart/form-data">
    请选择文件：<input type="file" name="attach"/><br/>
    <input type="submit" value="开始上传"/>
</form>


UploadController.java:
@RestController
public class UploadController {
	
    Map<String,Object> result = new HashMap<String,Object>();
	/*
	 * 接收文件
	 */
    @RequestMapping("/uploadAttach")
    public Map<String,Object> upload(@RequestParam("attach")MultipartFile file) throws Exception{
        //处理文件
        System.out.println("文件原名称："+file.getOriginalFilename());
        System.out.println("文件类型："+file.getContentType());
		
        file.transferTo(new File("d:/"+file.getOriginalFilename()));
		
        result.put("success", true);
        return result;
    } 
}
```

```
//Servlet

Web.xml(只要註冊Controller檔案):
<servlet-mapping>
    <servlet-name>EmpServlet</servlet-name>
    <url-pattern>/emp/emp.do</url-pattern>
</servlet-mapping>


select_page.jsp:(丟請求參數到Controller)
//!Action的第一步是到xml找相對應的Controller檔案，Action後的名稱要寫在xml檔裡面
//然後Controller再轉網頁
<FORM METHOD="post" ACTION="emp.do" >  
    <b>輸入員工編號 (如7001):</b>
    <input type="text" name="empno">
    <input type="hidden" name="action" value="getOne_For_Display">
    <input type="submit" value="送出">
</FORM>


EmpServlet.java:(1.接收請求參數-輸入格式的錯誤處理 2.查詢資料 3.查詢完成,準備轉交)
/***************************來自select_page.jsp的請求******************************/
if ("getOne_For_Display".equals(action)) { // 

/***************************查詢完成,準備轉交(Send the Success view)***************/
req.setAttribute("empVO", empVO); // 資料庫取出的empVO物件,存入req
String url = "/emp/listOneEmp.jsp";
RequestDispatcher successView = req.getRequestDispatcher(url); // 成功轉交 listOneEmp.jsp
successView.forward(req, res);

/***************************其他可能的錯誤處理*************************************/
} catch (Exception e) {
    errorMsgs.add("無法取得資料:" + e.getMessage());
    RequestDispatcher failureView = req.getRequestDispatcher("/emp/select_page.jsp");
    failureView.forward(req, res);
    }
}
```

### Spring Boot整合Servlet、Filter、Listener 
> @WebServlet、@WebFilter、@WebListener、@ServletComponentScan

SpringBoot使用Servlet API的兩種方法:
1.使用@ServletComponentScan註解(會去掃描@WebServlet、@WebFilter、@WebListener等註解)
2.使用@Bean註解

#### (02)使用@ServletComponentScan註解寫法

#HelloServlet主程式 (@WebServlet)
```
// @WebServlet:声明该类为Servlet程序
@WebServlet(name="helloServlet",urlPatterns="/helloServlet")  
/*
 * 等同於web.xml配置
 *     <servlet>
 *         <servlet-name>helloServlet</servlet-name>
 *         <servlet-class>cn.sm1234.servlet.HelloServlet</servlet-class>
 *     </servlet>
 *     <servlet-mapping>
 *     	   <servlet-name>helloServlet</servlet-name>
 *         <url-pattern>/helloServlet</url-pattern>
 *     </servlet-mapping>
 */
 
public class HelloServlet extends HttpServlet{

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
	System.out.println("执行了HelloServlet的doGet方法....");
    }
}
```
#Application啟動器 (@ServletComponentScan)
```
@SpringBootApplication
@ServletComponentScan  //@ServletComponentScan:作用让SpringBoot扫描@WebServlet等注解
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```
#HelloFilter過濾器 (@WebFilter)
```
//urlPatterns為攔截路徑，所以訪問此路徑會先經過過濾器
@WebFilter(filterName="helloFilter",urlPatterns="/helloServlet") //urlPatterns=攔截路徑
public class HelloFilter implements Filter{

    @Override
    public void destroy() {
		
    }

    @Override
    public void doFilter(ServletRequest arg0, ServletResponse arg1, FilterChain arg2)
        throws IOException, ServletException {
            System.out.println("执行了前面代码");
		
            //EX:arg2.doFilter(request, response);//放行，遞交給下一個過濾器
            //放行执行目标资源：HelloServlet
            arg2.doFilter(arg0, arg1);
		
            System.out.println("执行了后面代码");
        }

	@Override
	public void init(FilterConfig arg0) throws ServletException {
		
	}
}
```

#HelloListener監聽器 (@WebListener)
```
@WebListener
public class HelloListener implements ServletContextListener{

    @Override
    public void contextDestroyed(ServletContextEvent arg0) {
        System.out.println("ServletContext对象消耗了");
    }

    @Override
    public void contextInitialized(ServletContextEvent arg0) {
        System.out.println("ServletContext对象创建了");
    }
}
```
Console
```
ServletContext对象创建了
执行了前面代码
执行了HelloServlet的doGet方法....
执行了后面代码
```

#### (03)使用@Bean註解寫法
> @Bean
> 其他支程式寫法皆相同，只有啟動器要改變。

#Application啟動器 (@Bean)
```
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
	
    //注册Servlet程序
    @Bean
    public ServletRegistrationBean getServletRegistrationBean(){
        ServletRegistrationBean bean = new ServletRegistrationBean(new HelloServlet());
    //设置访问路径
        bean.addUrlMappings("/helloServlet");
        return bean;
    }
	
    //注册Filter
    @Bean
    public FilterRegistrationBean getFilterRegistrationBean(){
        FilterRegistrationBean bean = new FilterRegistrationBean(new HelloFilter());
    //过滤器拦截路径
        bean.addUrlPatterns("/helloServlet");
        return bean;
    }
	
    //注册Listener
    @Bean
    public ServletListenerRegistrationBean<HelloListener> getServletListenerRegistrationBean(){
        ServletListenerRegistrationBean<HelloListener> bean = new ServletListenerRegistrationBean<HelloListener>(new HelloListener());
        return bean;
    }
}
```
### (04)Spring Boot訪問靜態資源
1. src/main/resources > Create Folder(name:static) 
2. put xxx.jpg
3. visit localhost:8081/xxx.jpg
(static指的就是根目錄，不用打在路徑上)

4. visit html page
```
<html>
<head>
<meta charset="UTF-8">
<title>测试页面</title>
</head>
<body>
测试页面

<hr/>

<img src="images/mm.jpg"/>
</body>
</html>
```
### (05)Spring Boot實現文件上傳

> @RequestParam
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>文件上传页面</title>
</head>
<body>
文件上传页面

<hr/>
<form action="uploadAttach" method="post" enctype="multipart/form-data">
    请选择文件：<input type="file" name="attach"/><br/>
    <input type="submit" value="开始上传"/>
</form>
</body>
</html>
```


```
//使用@RequestParam因為參數名不相同，要更改接收參數名。
//也可改成MultipartFile attach，就不需要，@RequestParam了，如B TYPE:

A TYPE:
@RestController
public class UploadController {
	
    Map<String,Object> result = new HashMap<String,Object>();
	/*
	 * 接收文件
	 */
    @RequestMapping("/uploadAttach")
    public Map<String,Object> upload(@RequestParam("attach")MultipartFile file) throws Exception{
        //处理文件
        System.out.println("文件原名称："+file.getOriginalFilename());
        System.out.println("文件类型："+file.getContentType());
		
        file.transferTo(new File("d:/"+file.getOriginalFilename()));
		
        result.put("success", true);
        return result;
    } 
}

```
```
B TYPE:
@RestController
public class UploadController {
	
    Map<String,Object> result = new HashMap<String,Object>();
	/*
	 * 接收文件
	 */
    @RequestMapping("/uploadAttach")
    public Map<String,Object> upload(MultipartFile attach) throws Exception{
        //处理文件
        System.out.println("文件原名称："+attach.getOriginalFilename());
        System.out.println("文件类型："+attach.getContentType());
		
        //保存到硬盘
        attach.transferTo(new File("d:/"+attach.getOriginalFilename()));
        
        result.put("success", true);
        return result;
    } 
}

```

```
//因Spring Boot上傳文件限制不超過10M，故需修改application.properties File為

spring.http.multipart.maxFileSize=100MB <單個文件大小>
spring.http.multipart.maxRequestSize=200MB <整個請求大小，可包含多個文件>
```

### (06)Spring Boot整合Freemarker頁面模板
> 網頁發起請求 > 找到Controller > Controller丟回list > list內容在網頁上呈現

1.導入Freemarker啟動器(Jar包)
```
    <dependencies>
        <!-- web支持，SpringMVC， Servlet支持等 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!-- freemarker -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-freemarker</artifactId>
        </dependency>
    </dependencies>
```
2.建立VO
```
public class User {
    private Integer id;
    private String name;
    private Integer age;
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public Integer getAge() {
        return age;
    }
    public void setAge(Integer age) {
        this.age = age;
    }
    public User() {
        super();
    // TODO Auto-generated constructor stub
    }
    public User(Integer id, String name, Integer age) {
        super();
        this.id = id;
        this.name = name;
        this.age = age;
    }
	
}
```
3.建立Controller
```
@Controller
public class UserController {

    @RequestMapping("/list")
    public String list(Model model){
        //模拟用户数据
        List<User> list = new ArrayList<User>();
        list.add(new User(1,"小张",18));
        list.add(new User(2,"小徐",20));
        list.add(new User(3,"小陈",22));
		
        //把数据存入model
        model.addAttribute("list", list);
	
        //跳转到freemarker页面: list.ftl
        return "list";
    }
}
```
4.頁面模板放置固定位置src/main/resources/templates/
```
//freemarker模板副檔名為.ftl
//freemarker <#list>標籤可以迭代數據，如<#list 集合名 as 迭代出的物件代號>

<html>
    <title>用户列表展示</title>
    <meta charset="utf-8"/>
    <body>
        <h3>用户列表展示</h3>
        <table>
            <tr>
                <th>编号</th>
                <th>姓名</th>
                <th>年龄</th>
            </tr>
            <#list list as user>
            <tr>
                <td>${user.id}</td>
                <td>${user.name}</td>
                <td>${user.age}</td>
            </tr>
            </#list>
        </table>
	</body>
</html>
```

### (07)Spring Boot整合JSP頁面
> 同上，只有網頁寫法不同，其餘程式都相同

1.導入JSP啟動器(Jar包)
```
<dependencies>
    <!-- web支持，SpringMVC， Servlet支持等 -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- jsp依赖 -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
    </dependency>
    
    <dependency>
        <groupId>org.apache.tomcat.embed</groupId>
        <artifactId>tomcat-embed-jasper</artifactId>
        <scope>provided</scope>
    </dependency>
</dependencies>
```
2.application.properties設定
```
spring.mvc.view.prefix=/WEB-INF/jsp/
spring.mvc.view.suffix=.jsp
```


3.JSP頁面放置位置src/main/webapp/WEB-INF/jsp/
```
<%@ page language="java" contentType="text/html; charset=utf-8"
    pageEncoding="utf-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

<html>

<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>用户列表展示</title>
</head>

<body>
<h3>用户列表展示</h3>
    <table border="1">
        <tr>
            <th>编号</th>
            <th>姓名</th>
            <th>年龄</th>
        </tr>
        <c:forEach items="${list}" var="user">
        <tr>
            <td>${user.id}</td>
            <td>${user.name}</td>
            <td>${user.age}</td>
        </tr>
        </c:forEach>
    </table>
</body>

</html>

```

### (08)Spring Boot整合Thymeleaf

> 變量輸出、條件判斷、迭代遍歷、scope對象存取、超連結語法

1.導入Thymeleaf啟動器(Jar包)
```
    <dependencies>
        <!-- web支持，SpringMVC， Servlet支持等 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- thymeleaf -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
    </dependencies>
    
    
/升級版本，避免Meta標籤問題
    <properties>
        <java.version>1.7</java.version>
        <!-- 修改thymeleaf的版本 -->
        <thymeleaf.version>3.0.2.RELEASE</thymeleaf.version>
        <thymeleaf-layout-dialect.version>2.0.4</thymeleaf-layout-dialect.version>
    </properties>
```

2.頁面模板放置固定位置src/main/resources/templates/xxx.html

3.Controller

> 在Controller使用 model.addAtrribute = 把東西放在model裡面。然後在html頁面上就可以用th:text獲取到。
```
@Controller
public class UserController {

	@RequestMapping("/demo1")
	public String demo1(Model model){
		model.addAttribute("message", "你好，Thymeleaf");
		//跳转到templates/demo1.html
		return "demo1";
	}
	
	//变量输出
	@RequestMapping("/demo2")
	public String demo2(Model model){
		model.addAttribute("name", "张三");
		return "demo2";
	}
	
	//条件判断
	@RequestMapping("/demo3")
	public String demo3(Model model){
		model.addAttribute("gender", "女");
		
		model.addAttribute("grade",3);
		return "demo2";
	}
	
	//迭代遍历
	@RequestMapping("/demo4")
	public String demo4(Model model){
		List<User> list = new ArrayList<User>();
		list.add(new User(1,"eric",20));
		list.add(new User(2,"jack",22));
		list.add(new User(3,"rose",24));
		
		model.addAttribute("list", list);
		
		return "demo2";
	}
	
	//域对象的获取
	@RequestMapping("/demo5")
	public String demo5(HttpServletRequest request,Model model){
		
		//request
		request.setAttribute("request", "request's data");
		
		//session
		request.getSession().setAttribute("session", "session's data");
		
		//application
		request.getSession().getServletContext().setAttribute("application", "application's data");
		
		return "demo2";
	}
	
}
```
4.demo2.html
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Thymeleaf语法</title>
</head>
<body>

<h3>变量输出</h3>
<h4 th:text="${name}"></h4>
<h4 th:text="李四"></h4>

<hr/>

<h3>条件判断</h3>
<div th:if="${gender} == '男'">
	这是一位男性朋友
</div>
<div th:if="${gender} == '女'">
	这是一位女性朋友
</div>
<br/>
<div th:switch="${grade}">
	<span th:case="1">这是1的情况</span>
	<span th:case="2">这是2的情况</span>
	<span th:case="3">这是3的情况</span>
</div>

<hr/>

<h3>迭代遍历</h3>
<table border="1">
	<tr>
		<td>编号</td>
		<td>姓名</td>
		<td>年龄</td>
	</tr>
	<tr th:each="user : ${list}">
		<td th:text="${user.id}"></td>
		<td th:text="${user.name}"></td>
		<td th:text="${user.age}"></td>
	</tr>
</table>

<hr/>

<h3>域对象数据的获取</h3>
request: <span th:text="${#httpServletRequest.getAttribute('request')}"></span><br/>
session: <span th:text="${session.session}"></span><br/>
application: <span th:text="${application.application}"></span><br/>

<hr/>

// <a th:href="@{~/demo1}">访问demo1</a><br/>   ~ = 項目路徑
// 傳遞參數，類似傳統get請求，會把參數顯示在URL上

<h3>超链接的语法</h3>
<a th:href="@{~/demo1}">访问demo1</a><br/>

<a th:href="@{~/demo1(id=1,name=eric)}">访问demo1,传递参数</a>
</body>
</html>
```



4.demo1.html
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>一个Thymeleaf入门案例</title>
</head>
<body>

<span th:text="${message}"></span>

</body>
</html>
```

### (09)SpringBoot整合Mybatis