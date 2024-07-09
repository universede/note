### Optional类
- 简述
   &nbsp;&nbsp;<font color=RoyalBlue>NullPointerException</font>是Java最常见的异常之一，一直困扰着Java程序员。一方面程序员需要在代码中对null进行逻辑检查；另一方面，其属于运行时异常，是难以判断的。  
   &nbsp;&nbsp;引入Optional类，是通过使用检查空值的方式来防止代码污染。   
   &nbsp;&nbsp;<font color=RoyalBlue>Optional</font>类位于*java.util*的包下，可以为null的容器，如果值存在则*isPresent()*方法返回*true*，调用get()方法返回该对象。   

- 创建Optional对象
   &nbsp;&nbsp;在Optional类中，其构造器是私有的，故不可使用<font color=SandyBrown>new</font>创建对象，具体代码如下：
   ```java
     /**
     * Constructs an empty instance.
     *
     * @implNote Generally only one empty instance, {@link Optional#EMPTY},
     * should exist per VM.
     */
      private Optional() {
          this.value = null;
      }
    
     /**
     * Constructs an instance with the value present.
     *
     * @param value the non-null value to be present
     * @throws NullPointerException if value is null
     */
     private Optional(T value) {
        this.value = Objects.requireNonNull(value);
     }
   ```
   但可以通过以下方法来创建对象，即：
   - <font color=HotPink>Optional.of(T t)</font>：创建一个Optional对象，参数t不能为空
   - <font color=HotPink>Optional.empty()</font>：创建一个空的Optional实例
   - <font color=HotPink>Optional.ofNullable(T t)</font>：创建一个Optional对象，参数t可以为空
   Tips：<font color=Peru>of()</font>方法中的参数可以为空对象，但不能为null，如果为null，则会引出NullPointerException异常

- 方法
   - <font color=Orchid>boolean isPresent()</font>：判断是否包换对象
   - <font color=Orchid>void ifPresent(Consumer<? super T) consumer)</font>：如果有值，就执行 Consumer 接口的实现代码，并且该值会作为参数传递给它
   - <font color=Orchid>T get()</font>：如果调用对象包含值，返回该值，否则抛出异常
   - <font color=Orchid> T orElse(T other)</font>：如果有值则将其返回，否则返回指定的other 对象
   - <font color=Orchid>T orElseGet(Supplier<? extends T> other)</font>：如果有值则将其返回，否则返回由Supplier接口实现提供的对象
   - <font color=Orchid>T orElseThrow(Supplier<? extends X> exceptionSupplier)</font>：如果有值则将其返回，否则抛出由Supplier接口实现提供的异常

- 参考文献
[1] https://www.imooc.com/wiki/javalesson/optional.html
[2] https://www.baeldung.com/java-optional