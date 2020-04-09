```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans 
    xmlns="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xmlns:beans="http://www.springframework.org/schema/beans"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <!--
        Spring-WebMVC的DispatcherServlet环境配置: 定义处理请求的框架信息 
    -->
    
     <!-- 它背后注册了很多用于解析注解的处理器,其中就包括<context:annotation-config/>配置的注解所使用的处理器 -->
     <!-- 所以配置了<context:component-scan base-package="">之后,便无需再配置<context:annotation-config> -->  
     <context:component-scan base-package="com.papio"/>  
     
    <!-- 由 Spring进行扫描, 启用 Spring MVC 自动扫描 @Controller 注解的编程模型 --> 
     <!-- 启用SpringMVC的注解功能,它会自动注册HandlerMapping、HandlerAdapter、ExceptionResolver的相关实例 -->
    <annotation-driven />
    
    <!-- 扫描的base包 -->
    <context:component-scan base-package="com.sinog2c.mvc.controller,com.sinog2c.query.mvc.controller">
        <!--  将service排除在外，意味着MVC中不初始化service,防止事务失效  -->
        <context:exclude-filter type="annotation"
            expression="org.springframework.stereotype.Service" />
    </context:component-scan>
    
    <interceptors>
        <!-- 使用bean定义一个Interceptor，拦截所有的 *.action请求; 此处顺序即为拦截器链的顺序-->
        <beans:bean class="com.sinog2c.mvc.interceptor.LoginCheckInterceptor">
            <beans:property name="excludeList">
                <beans:list>
                    <beans:value>/login.action</beans:value>
                    <beans:value>/logout.action</beans:value>
                    <beans:value>/loginPage.page</beans:value>
                        <!--....... --> 
                </beans:list>
            </beans:property>
        </beans:bean> 
    </interceptors>
    
    <!-- JSP视图解析器,根据 @Controller 返回的视图名字转换到 /JSP/xxxx1/xxx2.jsp 文件  -->
    <!-- 配置SpringMVC的视图解析器 -->  
    <!-- 其viewClass属性的默认值就是org.springframework.web.servlet.view.JstlView -->  
    <beans:bean
        class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <beans:property name="prefix" value="/WEB-INF/JSP/" />
        <beans:property name="suffix" value=".jsp" />
    </beans:bean>

     <!-- 默认访问跳转到登录页面(即定义无需Controller的url<->view直接映射) -->  
    <mvc:view-controller path="/" view-name="forward:/login.jsp"/> 


    <!-- 由于web.xml中设置是：由SpringMVC拦截所有请求,于是在读取静态资源文件的时候就会受到影响(说白了就是读不到) -->  
    <!-- 经过下面的配置，该标签的作用就是：所有页面中引用"/js/**"的资源，都会从"/resources/js/"里面进行查找 -->  
    <!-- 我们可以访问http://IP:8080/xxx/js/my.css和http://IP:8080/xxx/resources/js/my.css对比出来 -->  
    <mvc:resources mapping="/js/**" location="/resources/js/"/>  
    <mvc:resources mapping="/css/**" location="/resources/css/"/>  
    <mvc:resources mapping="/WEB-INF/**" location="/WEB-INF/"/>  


    <!--  文件上传处理器,申明的id必须为multipartResolver  -->
    <beans:bean id="multipartResolver"
        class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <!-- 
            允许上传的最大文件大小，100M字节。当设为-1时表示无限制，默认是-1, 
        -->
        <beans:property name="maxUploadSize" value="-1" />
        <!-- 在文件上传时允许写到内存中的最大值，以字节为单位计算，默认是10240        -->
        <beans:property name="maxInMemorySize" value="4096" />
        <!-- 上传文件时的临时目录，默认是Servlet容器的临时目录 -->
    </beans:bean>

    <!-- 错误处理器 -->
    <beans:bean id="exceptionResolver" class="com.sinog2c.mvc.errorhandler.ExceptionHandler" />
    
    <!-- 异常映射 -->
     <!-- SpringMVC在超出上传文件限制时，会抛出org.springframework.web.multipart.MaxUploadSizeExceededException -->  
    <!-- 该异常是SpringMVC在检查上传的文件信息时抛出来的，而且此时还没有进入到Controller方法中 -->  
    <beans:bean  class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
        <beans:property name="exceptionMappings">
            <beans:props>
                <!-- 当抛出NumberFormatException时返回名叫number的视图 -->
                <beans:prop key="NumberFormatException">number</beans:prop>
                <beans:prop key="NullPointerException">null</beans:prop>
                 <!-- 遇到MaxUploadSizeExceededException异常时，自动跳转到/WEB-INF/error_fileupload.jsp页面 -->  
                <beans:prop key="MaxUploadSizeExceededException">WEB-INF/error_fileupload</beans:prop>
                  <!-- 处理其它异常(包括Controller抛出的) -->  
                <prop key="java.lang.Throwable">WEB-INF/500</prop>
            </beans:props>
        </beans:property>
        <!-- 当抛出异常但没有在exceptionMappings里面找到对应的异常时 返回名叫exception的视图 -->
        <beans:property name="defaultErrorView" value="exception" />
        <!-- 定义在发生异常时视图跟返回码的对应关系 -->
        <beans:property name="statusCodes">
            <beans:props>
                <!-- 发生NumberFormatException时返回视图number，对应HttpServletResponse的返回码500 -->
                <beans:prop key="number">500</beans:prop>
                <beans:prop key="null">503</beans:prop>
            </beans:props>
        </beans:property>
        <!-- 发生异常时默认的HttpServletResponse的返回码，默认是200 -->
        <beans:property name="defaultStatusCode" value="404" />
    </beans:bean>

    <!-- Jackson转换器 -->
    <beans:bean id="mappingJacksonHttpMessageConverter"
        class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter" />
    <!-- enum枚举值的引用方法 -->
    <beans:bean id="DisableCircularReferenceDetect" class="org.springframework.beans.factory.config.FieldRetrievingFactoryBean" >
        <beans:property name="staticField" value="com.alibaba.fastjson.serializer.SerializerFeature.DisableCircularReferenceDetect"></beans:property>
    </beans:bean>
    <beans:bean id="WriteNullStringAsEmpty" class="org.springframework.beans.factory.config.FieldRetrievingFactoryBean" >
        <beans:property name="staticField" value="com.alibaba.fastjson.serializer.SerializerFeature.WriteNullStringAsEmpty"></beans:property>
    </beans:bean>
    <beans:bean id="WriteNullNumberAsZero" class="org.springframework.beans.factory.config.FieldRetrievingFactoryBean" >
        <beans:property name="staticField" value="com.alibaba.fastjson.serializer.SerializerFeature.WriteNullNumberAsZero"></beans:property>
    </beans:bean>
    <beans:bean id="WriteMapNullValue" class="org.springframework.beans.factory.config.FieldRetrievingFactoryBean" >
        <beans:property name="staticField" value="com.alibaba.fastjson.serializer.SerializerFeature.WriteMapNullValue"></beans:property>
    </beans:bean>
    <!-- fastjson转换器 -->
    <beans:bean id="fastJsonHttpMessageConverter"
        class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter" >
        <!-- 避免IE执行AJAX时,返回JSON出现下载文件 -->
        <beans:property name="supportedMediaTypes">
            <beans:list>
                <beans:value>text/html;charset=UTF-8</beans:value>
            </beans:list>
        </beans:property>
        <!-- 转换时的特性设置 -->
        <beans:property name="features">
            <beans:array>
                <!-- 避免默认的循环引用替换 -->
                <beans:ref bean="DisableCircularReferenceDetect" />
                <beans:ref bean="WriteNullStringAsEmpty" />
                <beans:ref bean="WriteNullNumberAsZero" />
                <beans:ref bean="WriteMapNullValue" />
            </beans:array>
        </beans:property>
    </beans:bean>
    <beans:bean
        class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter">
        <beans:property name="messageConverters">
            <beans:list>
                <!-- json转换器 -->
                <beans:ref bean="fastJsonHttpMessageConverter" />
            </beans:list>
        </beans:property>
    </beans:bean>
</beans:beans>
```

