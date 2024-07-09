# ktuser

  把ktUser换成mybatis-plus
  
引依赖
 ```java
  <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.4.2</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.22</version>
            <scope>provided</scope>
        </dependency>
 ```
 
实体类DO
BaseDO
```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@SuperBuilder
@TableName("auth_user")
public class BaseDO {
    private String id;
    private Integer delFlag;
    private String addUserId;
    private String updateUserId;
    private Date addTime;
    private Date updateTime;
}
```

UserAuthDO
```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@SuperBuilder
public class UserAuthDO extends BaseDO {
    private String name;
    private String password;
    private String nickname;
    private String phone;
    private String email;

    public static final String PHONE = "phone";
    public static final String PASSWORD = "password";
}
```

自定义配置
```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@Component
@PropertySource(value = "kt-token.properties")
@ConfigurationProperties(prefix = "spring.kt-token")
@Builder
public class CustomerConfig {
    @JsonProperty(value = "token-name")
    private String tokenName;
    @JsonProperty(value = "timeout")
    private Long timeout;
    @JsonProperty(value = "allow-concurrent-login")
    private boolean allowConcurrentLogin;
    @JsonProperty(value = "jdbc-url")
    private String jdbcUrl;
    @JsonProperty(value = "jdbc-username")
    private String jdbcUsername;
    @JsonProperty(value = "jdbc-password")
    private String jdbcPassword;
    @JsonProperty(value = "cookie-time-out")
    private String cookieTimeOut;
    @JsonProperty(value = "cookie-domain")
    private String cookieDomain;
}
```
