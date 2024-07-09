# mybatis-plugin-excutor-sequece

### 问题引入
   当自定义日志插件遇到分页插件，自定义日志插件在执行SQL语句时不打印SQL语句的问题，可能在排错时，需要花费更多的时间。  
部分源码如下：  
```xml
<configuration>
   .....
   <plugins>
      <plugin interceptor = "com.xxx.CustomerLog" />
      <plugin interceptor="com.github.pagehelper.PageInterceptor" /> 
   </plugins>
</configuration>
```

### 分析  
  第一，插件没有生效，直接被放行，没被拦截到；第二，插件生效了，但直接放行了；第三，插件生效了，但不是日志的拦截器，而是其他的拦截器引起了SQL语句没打印直接放行了。显然这里不打印SQL语句属于第三这种情况。在Mybatis中使用到了责任链模式，Plugin的加载顺序是从上到下的，而执行的顺序是最先执行最外层，然后到最内层。在分页插件中，没有向下传递的方法，导致执行完后，直接把结果返回，没有再执行SQL打印日志的插件。  

### 解决方案  
```xml
<configuration>
   .....
   <plugins>
      <plugin interceptor="com.github.pagehelper.PageInterceptor" />
      <plugin interceptor = "com.xxx.CustomerLog" /> 
   </plugins>
</configuration>
```

### 参考文献  
[1] https://blog.csdn.net/qq_18433441/article/details/84036317