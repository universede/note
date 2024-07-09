# springboot-starer-processor

### 问题引入
  在SpringCloud工程中，都会把公共代码给抽离出来用于作为公共模块，方便复用。现在很多模块依赖于公共模块，在公共模块有一个通过token获取userId的方法，但是为了安全性，会对token拼接一些前缀之类的变量，这个变量可以是静态字符串，也可以是动态的配置。现在我需要在一个工具类中获取到配置文件中的前缀，但是都会引出空指针的问题。  
 公共模块源码如下：  
 CustomerDTO.java:  
 ```java
 @Component
 public class CustomerDTO {
    @Value(value="${spring.jdbc.kt-token}")
    private String tokenName;
 }
 ```
 HttpUtil.java  
 ```java
public class HttpUtil {
     public String getUserIdByToken(String token) {
        CustomerDTO bean = SpringUtil.getBean(CustomerDTO.class); 
        return RedisUtil.get(bean.getTokenName + ":" + token);
     }
}
 ```

### 分析[^1]
   在Spring中，对象的创建都是交由Spring框架来管理的，报空指针相关的问题，绝大部分问题是因为对象没有被创建。而在我这里对象是创建成功了的，相对于子模块来说，但子模块依赖了公共模块。子模块虽然依赖了公共模块，可以使用里面的工具类，但是CustomerDTO类中使用到了注解，子模块的启动类中并没有对其进行扫描，@SpringBootApplication中的注解之作用于子模块自身，如果引入第三方包时，第三方包里的组件、配置等并不会被容器进行管理，这时就需要使用注解中的scanBasePackage属性，为需要的地方手动扫包。  
   
### 参考文献
[^1]:https://blog.csdn.net/znzbs/article/details/123466373