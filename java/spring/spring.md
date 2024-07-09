# Spring Source

### 定义
&emsp;是一种后端框架，为了解决企业级开发项目时项目复杂性，方便项目之间的解耦。
### 下载
1. 源码[^1]，[Spring5.3](https://github.com/spring-projects/spring-framework/tree/5.3.x)
2.  Gradle编译器[^2]，[Gradle](https://gradle.org/install/)
3.  环境配置[^3][^4][^5]
     - JDK 17, Gradle 7.2(安装路径自己指定，网上有教程，不多详述)
     - 步骤
        &emsp;打开spring源码文件，修改gradle/wrapper目录下的<font color=#F0E68C>gradle-wrapper.properties文件中的**distributionUrl**的路径为(自己下载的gradle压缩包的路径)：
        ```
        distributionUrl=file\:///media/universe/_dde_data/application/library/gradle/gradle-7.2-all.zip
        ```
        &emsp;编译之前，如果是当前最新版的spring源码，最好不要修改下载源地址，如果修改可能会出现找不到jar包的情况，导致找不到什么原因引起编译失败，执行编译命令，```./gradlew build```
        &emsp;执行,```./gradlew :spring-oxm:compileTestJava```
        &emsp;自定义模块(这里面肯定需要引入其sping源码的模块文件)，需要注意```compile(project(":spring-context"))```
和```implementation(project(":spring-context"))```的引入区别[^6]

### 基本架构流程分析图
![spring](vx_images/3613757259296.png =801x)

### 源码分析
 * 加载过程
  String[] -> String -> Resource[] -> Resource -> Document -> 解析文档中的节点

### 核心点-1
#### refresh()[^7]
&emsp;主要完成12件事情，参照以下：
 + 容器刷新前的准备, 即```prepareRefresh();```
 + 初始化beanFactory，加载并解析配置，即```ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();```
 + 设置beanFactory的属性，即```prepareBeanFactory(beanFactory);```
 + BeanFactory创建完成进行的后置处理工作，即```postProcessBeanFactory(beanFactory);```
 + 执行BeanFactoryPostProcessor的方法，即 ```invokeBeanFactoryPostProcessors(beanFactory);```
 + 注册BeanPostProcessor，即```registerBeanPostProcessors(beanFactory);beanPostProcess.end();```
 + 初始化MessageSource组件，即```initMessageSource();```
 + 初始化事件派发器，即```initApplicationEventMulticaster();```
 + 子类重写这个方式，在容器刷新的时候可以自定义逻辑，即```onRefresh();```
 + 将所有的ApplicationLinstener注册到容器中，即```registerListeners();```
 + 初始化所有剩下的单实例bean，即```finishBeanFactoryInitialization(beanFactory);```
 + 完成BeanFactory的初始化创建工作，IOC容器创建完成，即```finishRefresh();```

* prepareRefresh()[^7]
&emsp;主要完成以下事情：
  - 设置容器启动时间
  - 设置关闭为false
  - 设置激活为true
  - 获取Environment对象，并把系统环境设置到Environment对象中
  - 准备监听器和事件的集合对象，默认为null

```java

    protected void prepareRefresh() {
		// Switch to active.
		this.startupDate = System.currentTimeMillis();
		this.closed.set(false);
		this.active.set(true);

		if (logger.isDebugEnabled()) {
			if (logger.isTraceEnabled()) {
				logger.trace("Refreshing " + this);
			}
			else {
				logger.debug("Refreshing " + getDisplayName());
			}
		}

		// Initialize any placeholder property sources in the context environment.
		// 初始化属性，未实现，由自己自定义去实现
		initPropertySources();

		// Validate that all properties marked as required are resolvable:
		// see ConfigurablePropertyResolver#setRequiredProperties
		getEnvironment().validateRequiredProperties();

		// Store pre-refresh ApplicationListeners...
		if (this.earlyApplicationListeners == null) {
			this.earlyApplicationListeners = new LinkedHashSet<>(this.applicationListeners);
		}
		else {
			// Reset local application listeners to pre-refresh state.
			this.applicationListeners.clear();
			this.applicationListeners.addAll(this.earlyApplicationListeners);
		}

		// Allow for the collection of early ApplicationEvents,
		// to be published once the multicaster is available...
		this.earlyApplicationEvents = new LinkedHashSet<>();
	}
```

* obtainFreshBeanFactory()[^8]
&emsp;主要作用是读取配置文件，创建BeanFactory容器
```java
    
      protected ConfigurableListableBeanFactory obtainFreshBeanFactory() {
		     refreshBeanFactory();
		     return getBeanFactory();
	  }
	  @Override
	  protected final void refreshBeanFactory() throws BeansException {
		if (hasBeanFactory()) {
			destroyBeans();
			closeBeanFactory();
		}
		try {
			DefaultListableBeanFactory beanFactory = createBeanFactory();
			beanFactory.setSerializationId(getId());
			customizeBeanFactory(beanFactory);
			loadBeanDefinitions(beanFactory);
			this.beanFactory = beanFactory;
		}
		catch (IOException ex) {
			throw new ApplicationContextException("I/O error parsing bean definition source for " + getDisplayName(), ex);
		}
	}
```

### IOC


### AOP



### EXTENT
反射代码：通过反射创建对象的过程
pupulateBean
**调用aware接口的方法，使自定义对象方便获取容器对象**
- BeanFactory与FactoryBean的区别[^9]
  **BeanFactory**是一个容器的根入口，是按着严格的步骤创建Bean对象(11个步骤-refresh())；**FactoryBean**也能创建Bean对象,但不受Spring容器的管理，这里主要指不会走一个标准的Spring的生命周期
  


### 参考文献
[^1]:https://github.com/spring-projects/spring-framework/tree/5.3.x
[^2]:https://gradle.org/install/
[^3]:https://github.com/spring-projects/spring-framework/wiki/Build-from-Source
[^4]:https://blog.csdn.net/m0_58476806/article/details/118108115
[^5]:https://www.cnblogs.com/mazhichu/p/13163979.html
[^6]:https://blog.csdn.net/sinat_31057219/article/details/82799223
[^7]:https://www.freeaihub.com/post/107569.html
[^8]:https://zhuanlan.zhihu.com/p/80381784
[^9]:https://juejin.cn/post/7036691963822735390