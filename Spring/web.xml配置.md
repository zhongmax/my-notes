```xml
<?xml version="1.0" encoding="UTF-8"?>
 <!-- Web容器加载顺序ServletContext--context-param--listener--filter--servlet -->
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" version="2.5">
  <display-name>项目</display-name>
  
  <!-- 指定Spring的配置文件 -->  
    <!-- 否则Spring会默认从WEB-INF下寻找配置文件,contextConfigLocation属性是Spring内部固定的 -->
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:applicationContext*.xml</param-value>
  </context-param>
  
   <!-- 防止发生java.beans.Introspector内存泄露,应将它配置在ContextLoaderListener的前面 -->
   <listener>  
        <listener-class>org.springframework.web.util.IntrospectorCleanupListener</listener-class>  
  </listener>  
    
   <!-- 实例化Spring容器 -->  
    <!-- 应用启动时,该监听器被执行,它会读取Spring相关配置文件,其默认会到WEB-INF中查找applicationContext.xml -->
  <listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
  
  <!-- 解决乱码问题 -->  
    <!-- forceEncoding默认为false,此时效果可大致理解为request.setCharacterEncoding("UTF-8") -->  
    <!-- forceEncoding=true后,可大致理解为request.setCharacterEncoding("UTF-8")和response.setCharacterEncoding("UTF-8") -->
  <filter>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
      <param-name>forceEncoding</param-name>
      <param-value>true</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
  
  
<!--   WebStatFilter用于采集web-jdbc关联监控的数据。 -->
  <filter>
    <filter-name>DruidWebStatFilter</filter-name>
    <filter-class>com.alibaba.druid.support.http.WebStatFilter</filter-class>
    <init-param>
      <param-name>exclusions</param-name>
      <param-value>*.js,*.gif,*.jpg,*.png,*.css,*.ico,*.jsp,/druid/*,/download/*</param-value>
    </init-param>
    <init-param>
      <param-name>sessionStatMaxCount</param-name>
      <param-value>2000</param-value>
    </init-param>
    <init-param>
      <param-name>sessionStatEnable</param-name>
      <param-value>true</param-value>
    </init-param>
    <init-param>
      <param-name>principalSessionName</param-name>
      <param-value>session_user_key</param-value>
    </init-param>
    <init-param>
      <param-name>profileEnable</param-name>
      <param-value>true</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>DruidWebStatFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
  
   <!-- 配置Shiro过滤器,先让Shiro过滤系统接收到的请求 -->  
    <!-- 这里filter-name必须对应applicationContext.xml中定义的<bean id="shiroFilter"/> -->  
    <!-- 使用[/*]匹配所有请求,保证所有的可控请求都经过Shiro的过滤 -->  
    <!-- 通常会将此filter-mapping放置到最前面(即其他filter-mapping前面),以保证它是过滤器链中第一个起作用的 -->  
  <filter>
    <filter-name>shiroFilter</filter-name>
    <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
     <!--   <init-param>  
            该值缺省为false,表示生命周期由SpringApplicationContext管理,设置为true则表示由ServletContainer管理  
            <param-name>targetFilterLifecycle</param-name>  
            <param-value>true</param-value>  
        </init-param>   -->
  </filter>
  <filter-mapping>
    <filter-name>shiroFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
  
  
  <servlet>
    <servlet-name>DruidStatView</servlet-name>
    <servlet-class>com.alibaba.druid.support.http.StatViewServlet</servlet-class>
    <init-param>
      <param-name>resetEnable</param-name>
      <param-value>true</param-value>
    </init-param>
    <init-param>
      <param-name>loginUsername</param-name>
      <param-value>druid</param-value>
    </init-param>
    <init-param>
      <param-name>loginPassword</param-name>
      <param-value>druid</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>DruidStatView</servlet-name>
    <url-pattern>/druid/*</url-pattern>
  </servlet-mapping>
  
   <!-- SpringMVC核心分发器 --> 
  <servlet>
    <servlet-name>mvcServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:webmvc/servlet-context.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>mvcServlet</servlet-name>
    <url-pattern>*.action</url-pattern>
    <url-pattern>*.json</url-pattern>
    <url-pattern>*.page</url-pattern>
  </servlet-mapping>
  
<!--   webservice————Web 服务框架
  介绍：https://www.ibm.com/developerworks/cn/java/j-jws12.html -->
  <servlet>
    <servlet-name>cxf</servlet-name>
    <servlet-class>org.apache.cxf.transport.servlet.CXFServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>cxf</servlet-name>
    <url-pattern>/ws/*</url-pattern>
  </servlet-mapping>

   <!-- Session超时30分钟(零或负数表示会话永不超时)-->  
    <!--   
    <session-config>  
        <session-timeout>30</session-timeout>  
    </session-config>  
     -->  
  
    <!-- 默认欢迎页 -->
    <!-- Servlet2.5中可直接在此处执行Servlet应用,如<welcome-file>servlet/InitSystemParamServlet</welcome-file> -->  
    <!-- 这里使用了SpringMVC提供的<mvc:view-controller>标签,实现了首页隐藏的目的,详见applicationContext.xml -->  
    <!--   
    <welcome-file-list>  
        <welcome-file>login.jsp</welcome-file>  
    </welcome-file-list>  
     -->  
     <!-- 错误展示页面配置-->  
    <error-page>  
        <error-code>405</error-code>  
        <location>/WEB-INF/405.html</location>  
    </error-page>  
    <error-page>  
        <error-code>404</error-code>  
        <location>/WEB-INF/404.jsp</location>  
    </error-page>  
    <error-page>  
        <error-code>500</error-code>  
        <location>/WEB-INF/500.jsp</location>  
    </error-page>  
    <error-page>  
        <exception-type>java.lang.Throwable</exception-type>  
        <location>/WEB-INF/500.jsp</location>  
    </error-page>  
</web-app>
```