# exception
```
2021-07-01T08:39:32+08:00--INFO --[main] c.c.f.f.i.provider.DefaultApplicationProvider - App ID is set to 25008 by app.id property from /META-INF/app.properties
2021-07-01T08:39:32+08:00--INFO --[main] c.c.f.f.internals.provider.DefaultServerProvider - Loading /opt/settings/server.properties
2021-07-01T08:39:32+08:00--INFO --[main] c.c.f.f.internals.provider.DefaultServerProvider - Environment is set to [DEV] by property 'env' in server.properties.
2021-07-01T08:39:32+08:00--INFO --[main] c.c.f.f.internals.provider.DefaultServerProvider - Data Center is set to [wangxi] by property 'idc' in server.properties.
2021-07-01T08:39:32+08:00--INFO --[main] c.c.f.apollo.internals.DefaultMetaServerProvider - Located meta services from apollo.meta configuration: http://192.168.1.11:8080!
2021-07-01T08:39:32+08:00--INFO --[main] com.ctrip.framework.apollo.core.MetaDomainConsts - Located meta server address http://192.168.1.11:8080 for env DEV from com.ctrip.framework.apollo.internals.DefaultMetaServerProvider
2021-07-01T08:39:33+08:00--INFO --[main] c.b.l.userextend.LogisticsUserExtendApplication - No active profile set, falling back to default profiles: default
2021-07-01T08:39:41+08:00--INFO --[main] o.s.d.r.config.RepositoryConfigurationDelegate - Multiple Spring Data modules found, entering strict repository configuration mode!
2021-07-01T08:39:41+08:00--INFO --[main] o.s.d.r.config.RepositoryConfigurationDelegate - Bootstrapping Spring Data Redis repositories in DEFAULT mode.
2021-07-01T08:39:41+08:00--INFO --[main] o.s.d.r.config.RepositoryConfigurationDelegate - Finished Spring Data repository scanning in 73ms. Found 0 Redis repository interfaces.
2021-07-01T08:39:42+08:00--WARN --[main] o.springframework.boot.actuate.endpoint.EndpointId - Endpoint ID 'service-registry' contains invalid characters, please migrate to a valid format.
2021-07-01T08:39:42+08:00--INFO --[main] o.s.c.annotation.ConfigurationClassPostProcessor - Cannot enhance @Configuration bean definition 'com.ctrip.framework.apollo.spring.boot.ApolloAutoConfiguration' since its singleton instance has been created too early. The typical cause is a non-static @Bean method with a BeanDefinitionRegistryPostProcessor return type: Consider declaring such methods as 'static'.
2021-07-01T08:39:43+08:00--INFO --[main] o.springframework.cloud.context.scope.GenericScope - BeanFactory id=fb5bac23-48f2-34dd-ae5c-9966f1e4560b
2021-07-01T08:39:44+08:00--WARN --[main] o.s.boot.context.properties.PropertySourcesDeducer - Multiple PropertySourcesPlaceholderConfigurer beans registered [propertySourcesPlaceholderConfigurer, org.springframework.context.support.PropertySourcesPlaceholderConfigurer], falling back to Environment
2021-07-01T08:39:49+08:00--INFO --[main] o.s.boot.web.embedded.tomcat.TomcatWebServer - Tomcat initialized with port(s): 25008 (http)
2021-07-01T08:39:49+08:00--INFO --[main] org.apache.coyote.http11.Http11NioProtocol - Initializing ProtocolHandler ["http-nio-25008"]
2021-07-01T08:39:49+08:00--INFO --[main] org.apache.catalina.core.StandardService - Starting service [Tomcat]
2021-07-01T08:39:49+08:00--INFO --[main] org.apache.catalina.core.StandardEngine - Starting Servlet engine: [Apache Tomcat/9.0.36]
2021-07-01T08:39:50+08:00--INFO --[main] o.a.c.core.ContainerBase.[Tomcat].[localhost].[/] - Initializing Spring embedded WebApplicationContext
2021-07-01T08:39:50+08:00--INFO --[main] o.s.b.w.s.c.ServletWebServerApplicationContext - Root WebApplicationContext: initialization completed in 16832 ms
2021-07-01T08:39:52+08:00--WARN --[main] com.netflix.config.sources.URLConfigurationSource - No URLs will be polled as dynamic configuration sources.
2021-07-01T08:39:52+08:00--INFO --[main] com.netflix.config.sources.URLConfigurationSource - To enable URLs as dynamic configuration sources, define System property archaius.configurationSource.additionalUrls or make config.properties available on classpath.
2021-07-01T08:39:52+08:00--INFO --[main] com.netflix.config.DynamicPropertyFactory - DynamicPropertyFactory is initialized with configuration sources: com.netflix.config.ConcurrentCompositeConfiguration@3370f42
2021-07-01T08:39:53+08:00--WARN --[main] o.s.b.w.s.c.AnnotationConfigServletWebServerApplicationContext - Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'permissionCheckAspect' defined in URL [jar:file:/java_ceshi/logistics-user-extend.jar!/BOOT-INF/classes!/com/bdfint/logistics/userextend/config/PermissionCheckAspect.class]: Instantiation of bean failed; nested exception is java.lang.ExceptionInInitializerError
2021-07-01T08:39:54+08:00--INFO --[main] org.apache.catalina.core.StandardService - Stopping service [Tomcat]
2021-07-01T08:39:54+08:00--INFO --[main] o.s.b.a.l.ConditionEvaluationReportLoggingListener - 

Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2021-07-01T08:39:54+08:00--ERROR--[main] org.springframework.boot.SpringApplication - Application run failed
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'permissionCheckAspect' defined in URL [jar:file:/java_ceshi/logistics-user-extend.jar!/BOOT-INF/classes!/com/bdfint/logistics/userextend/config/PermissionCheckAspect.class]: Instantiation of bean failed; nested exception is java.lang.ExceptionInInitializerError
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.instantiateBean(AbstractAutowireCapableBeanFactory.java:1320)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBeanInstance(AbstractAutowireCapableBeanFactory.java:1214)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:557)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:517)
	at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:323)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:226)
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:321)
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:202)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:893)
	at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:879)
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:551)
	at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:143)
	at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:758)
	at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:750)
	at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:397)
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:315)
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1237)
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1226)
	at com.bdfint.logistics.userextend.LogisticsUserExtendApplication.main(LogisticsUserExtendApplication.java:21)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.springframework.boot.loader.MainMethodRunner.run(MainMethodRunner.java:49)
	at org.springframework.boot.loader.Launcher.launch(Launcher.java:109)
	at org.springframework.boot.loader.Launcher.launch(Launcher.java:58)
	at org.springframework.boot.loader.JarLauncher.main(JarLauncher.java:88)
Caused by: java.lang.ExceptionInInitializerError: null
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at org.springframework.beans.BeanUtils.instantiateClass(BeanUtils.java:204)
	at org.springframework.beans.factory.support.SimpleInstantiationStrategy.instantiate(SimpleInstantiationStrategy.java:87)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.instantiateBean(AbstractAutowireCapableBeanFactory.java:1312)
	... 26 common frames omitted
Caused by: java.lang.NullPointerException: null
	at com.bdfint.logistics.userextend.aware.SpringContextHolder.getBean(SpringContextHolder.java:53)
	at com.bdfint.logistics.userextend.config.PermissionCheckAspect.<clinit>(PermissionCheckAspect.java:40)
	... 33 common frames omitted
```

部署到服务器，启动报错；原因：<font color=#890545>Spring在实例化这个类的时候，先执行静态方法，此时某个类还未实例化(检查是否已加注解)，故而报了这个空指针错误。</font>
这里是在切面内使用到了
```
    private static IUserService iUserService = SpringContextHolderClass.getBean(IUserService.class);
    private static IRoleService iRoleService = SpringContextHolderClass.getBean(IRoleService.class);
```
执行过程中，spring容器并没有创建好容器，就使用了static的静态变量去获取这个对象，（spring使用懒加载）

使用setter注入或构造器注入


* 知识点
 spring的4种注入方法
  1. setter
  2. 构造器
  3. 使用自定义静态组件的方法
  4. 直接用Spring框架工具类获取bean
 [参考文献](https://blog.csdn.net/RogueFist/article/details/79575665)