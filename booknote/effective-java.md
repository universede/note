# effective-java

![effctive-java](vx_images/1124114605688.png =550x)
#### INSTRUCTION
  - java.lang
  - java.util
     * java.util.concurrent
     * java.util.function
  - java.io

  “<font color=#7980ED>反模式</font>”包含有一个或多个应该在实践中避免的程序示例。

#### 对象的创建和销毁
   - <font color=#72D3D9>用静态工厂方法代替构造器</font>
      **优势：**
            &emsp;1. 静态工厂方法有名称
            &emsp;2. 不必在每次调用的时候都创建一个对象
            &emsp;3. 返回原返回类型类型的任何子类型的对象
            &emsp;4. 所返回的对象的类可以随着每次调用而发生变化，这取决于静态工厂的参数值
            &emsp;5. 方法返回的对象所属的类，在编写包含该静态工厂方法的类时可以不存在
      **缺点：**
             &emsp;1. 类如果不含有公有的或者受保护的构造器，就不能被实例化
             &emsp;2. 程序员很难发现它们
  - <font color=#7070ED>遇到多个构造器参数时要考虑使用构建器</font>
      &emsp;<font color=#7070ED>构建器</font>:通过属性的字段自动构建需要的属性。
    ```java
        public class StaticFactory implements Serializable {

            private Integer id;
            private String name;
            private String data;

            public static class Builder {

                private Integer id = 0;
                private String name = "";
                private String data = "";

                public Builder() { }

                public Builder id(Integer id) {
                    this.id = id;
                    return this;
                }

                public Builder name(String name) {
                    this.name = name;
                    return this;
                }

                public Builder data(String data) {
                    this.data = data;
                    return this;
                }

                public StaticFactory build() {
                    return new StaticFactory(this);
                }
            }

            private StaticFactory() { }

            private StaticFactory(Builder builder) {
                this.id = builder.id;
                this.name = builder.name;
                this.data = builder.data;
            }

        }
        public class TestStaticFactory {
            public static void main(String[] args) {

                StaticFactory d = new StaticFactory.Builder()
                                .id(11)
                                .name("x")
                                .data("h")
                                .build();
                System.out.println(d.toString());
            }
        }
    ```
  - <font color=#70EDED>用私有构造器或者枚举类型强化Singleton属性</font>
     <font color=#70FDSD>Singleton:</font>仅被实例化一次的类，通常被用来代表一个无状态的对象，如函数或那些本质上唯一的系统组件。
  - <font color=#70DDED>通过私有构造器强化不可实例化的能力</font>
     让一个类包含一个私有构造器，这个类就不能再实例化。
  - <font color=#DF3DF4>优先考虑依赖注入来引入资源</font>
     当创建一个资源时，就将该资源传入到构造器中。 其中的一个变体就是<font color=#46EDED>工厂模式</font>，传入一个工厂到构造器，使其构造出其中的子类，如JDK1.8中的<font color=#78DEDE>Supplier<T></font>；但需要注意的是它会使大型项目混乱，这时就需要使用集成的框架，如Spring、Dagger、Guice
  - <font color>避免创建不必要的对象</font>
# 




