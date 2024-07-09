# xxl-job[^1]

#### 是什么
  &emsp;它是一个开源的<font color=#7080ED>分布式任务调度平台</font>，核心设计目标是<font color=#7070DE>开发迅速、简单学习、轻量级、易扩展</font>。

#### 特点
  - 简单
  - 动态
  - 调度中心HA(中心式)
  - 执行器HA(分布式)
  - 注册中心
  - 弹性扩容缩容
  - 触发策略
  - 调度过期策略
  - 阻塞处理策略
  - 任务超时控制
  - 任务失败重试
  - 任务失败告警
  - 路由策略
  - 分片广播任务
  - 动态分片
  - 故障转移
  - 任务进度监控
  - Rolling实时日志
  - GLUE
  - 脚本任务
  - 命令行任务
  - 任务依赖
  - 一致性
  - 自定义任务参数
  - 调度线程池
  - 数据加密
  - 邮件报警
  - 推送maven中央仓库
  - 运行报表
  - 全异步
  - 跨语言
  - 国际化
  - 容器化
  - 线程池隔离
  - 用户管理
  - 权限管理

#### 要素
   * 执行器
       执行任务的实例
   * 任务
      代码中的业务
   * 触发器
      配置的表达式，即<font color=#7070DE>cron</font>

#### 应用场景
   * 时间驱动
      - 房贷短信
      - 营销类短信
      - 对账单、日结
      - 统计图表
   * 数据驱动
      - 异步数据交换
      - 数据同步
      - 大数据作业
      - 电商业务
      - O2O业务

#### 任务框架[^2]
   + 单机
       1. timer
       2. ScheduledExcutorService
       3. spring定时框架

   + 分布式
       1. Quartz
       2. xxl-job
       3. TBSchedule
       4. elastic-job
       5. Saturn
       6. Azkaban[^3]

#### 原生定时任务框架的缺陷
   (1). 不支持分片任务
   (2). 不支持生命周期统一管理
   (3). 不支持集群
   (4). 不支持失败重试
   (5). 不支持动态调整
   (6). 无报警机制
   (7). 任务数据统计难以统计

#### 为什么使用
  &emsp;需要在某一特定的时刻去做某一件事。在企业级的系统中，所执行的任务多，时间不确定性，决定了使用代码的形式来管理定时任务是不可能的，这时就需要使用其它的方式来管理定时任务，如xxl-job任务调度平台。

#### 怎样使用
   * 原生框架代码示例
   ```java
    @Component
    @EnableScheduling
    public class MyJobHandler {

        @Scheduled(cron = "*/2 * * * * *")
        public void execute() throws Exception {
            System.out.println("我们不能失去信仰");
        }
    }
   ```
   * xxl-job
   ```java
   @Component
    public class MyJobXxlJob {
        private static transient Logger logger = LoggerFactory.getLogger(MyJobXxlJob.class);

        @XxlJob("jobHandler")
        public ReturnT<String> execute(String...param) throws Exception {
            logger.info("xxl-job===========");
            return ReturnT.SUCCESS;
        }
    }

   ```

#### 架构设计  
   * 设计思想  
     &emsp;将调度行为抽象形成“调度中心”公共平台，而平台自身并不承担业务逻辑，“调度中心”负责起发起调度请求。  
     &emsp;将任务抽象成分散的JobHandler，交由“执行器”统一管理，“执行器”负责接收调度并执行对应的JobHandler中业务逻辑。  
   * 架构图  
      ![xxl-job](https://www.xuxueli.com/doc/static/xxl-job/images/img_Qohm.png =600x)
   * 系统组成   
      - 调度模块(调度中心)  
      - 执行模块(执行器)  


#### 参考文献
[^1]:https://www.xuxueli.com/xxl-job/
[^2]:https://cloud.tencent.com/developer/article/1524768
[^3]:https://developer.aliyun.com/article/770088