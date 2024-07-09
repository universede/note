

#### 继承  

 - 继承的设计技巧  
   1. 将公有操作和域放入超类  
   2. 不要使用受保护的域  
   3. 使用继承实现“is-a”关系  
   4. 除非所有继承的方法都有意义，否则不要使用继承   
   5. 在覆盖方法时，不要改变预期的行为   
   6. 使用多态，而非类型信息   
   7. 不要过多的使用反射    

#### 接口   
  接口不是类，而是对类的一组需求描述，这些类要遵从接口描述的统一格式进行定义  
  接口没有实例   
  - 接口与抽象类  
    类可以有多个接口，但只能继承一个父类，原因是Java是一种单继承的语言   
  - 静态方式  
    使用**static**修饰的方法(类方法)，直接可使用类进行调用   
  - 默认方法   
    使用**default**修饰的方法，也可省略的修饰符   
  - 默认方法的解决方案
    同时实现两个不同的接口，而接口中的方法名等一致，在重写这些方法时，会遵循一定的规则，即：   
    1. 超类优先   
       如果一个超类提供了一个具体的方法，同名而且有相同参数类型的默认方法后被忽略  
    2. 接口冲突  
       如果一个超接口提供了一个默认方法，另一个接口也提供了一个同名而且有相同参数类型的默认方法，必须覆盖这个方法来解决问题  
  - Compareable接口  
       
  - 对象克隆  
     * 浅克隆  
 
     * 深克隆
  - lambda表达式和函数式编程  
     - lambda表达式  
        可传递的表达式  
        格式：参数 箭头(->) 表达式  
        闭包:lambda表达式   
        lambda表达式中只能引用值不能改变变量，因为并发执行多个动作时就会变得不安全  
        lambda表达式中捕获的变量必须实际上是最终变量   
        实际上的最终变量是指，这个变量初始化后就不会再为它赋值   
        使用lambda表达式是延迟执行   
        可以使用@FunctionInterface注解自定义接口   
     - 函数式接口  
        对于只有一个抽象方法的接口，需要这个接口的对象时，就可以提供一个lambda表达式。
     - 方法引用  
        表达式：System:out::println  
        用<font color=DeepSkyBlue>::</font>分隔方法名与对象或类名  
        ```java
            Object::instanceMethod
            class::staticMethod
            class:instanceMethod
        ```
        方法引用不能独立存在，总是会转化为函数接口的实例  
        this.instanceMethod
        super.instanceMethod   
        使用**this**作为目标，会调用给定方法的超类版本   
      - 构造器引用   
        和方法引用相似，但是方法名为**new**   
      - 内部类   
        内部类声明的静态域必须是final   
        内部类不能有static方法   
      - 局部内部类   
        局部内部类不能用public或private访问说明符进行声明   
        它的作用域限定在声明这个局部类的块中   
      - 匿名内部类  
        只创建这个类的一个对象，则不必命名了   
        匿名内部类没有构造器，而是将构造器参数传递给超类构造器   
      - 静态内部类  
        可以使用static修饰   
      - 代理   
        利用代理可以在运行时创建一个实现一组给定接口的新类   
        这种功能只能在编译时无法确定需要实现哪个接口时才有必要使用   
        一个代理类只有一个实例域--》调用处理器(invocation handler)
        它实现了InvocationHandler接口的类对象  
        Object invoke(Object proxy, Method method, Object[] args)     
        代理类一定是public和final   
         

#### 反射  
 - 定义 
   能够分析类能力的程序
 - 存放地方   
   java.lang.reflect    
 - 作用  
   * 在运行时分析类的能力   
   * 在运行时查看对象  
   * 实现通用的数组操心代码  
   * 利用Method对象  
 - 使用人员  
   工具构造者，而不是应用程序员  
 - Class类  
   获取Class类的两种方式：  
   - 对象名.getClass()   
   - Class.forName(String str); 
 - 反射创建对象   
   反射中提供了一个newInstance()的方法，可以通过**Class.forName().newInstance**形式创建一个想要的对象   
 - 利用反射获取类的域、方法、构造器  
   getField()、getMethod()、getContructors()等    
   

#### 异常   
 - 分类  
   异常(Exception)和错误(Error)，异常可以排查，并且解决，但错误有可能不能解决  
   异常：已检查异常和未检查异常  
   已检查异常:编译器将会检查是否提供处理器   
   未检查异常:访问null引用，如传递参数过程中，在某一个地方传递是的null数据，引发空指针异常  
 - 异常捕获方式  
   - 局部捕获  
     ```java
        try{
            code
        }catch(Exception e) {
            e.printStackTrace()；
        }finally {
            code
        }
     ```
     这是一种比较常用的捕获方式，其中有时为了更高效的使用捕获会使用最新的捕获方式，即**try(resource){...}catch(Exception e){e.printStackTrace()}finally{...}**   
    - 方法捕获   
      使用关键字**throws**抛出异常  
    - 语句捕获  
      使用关键字**throw**抛出异常  
      