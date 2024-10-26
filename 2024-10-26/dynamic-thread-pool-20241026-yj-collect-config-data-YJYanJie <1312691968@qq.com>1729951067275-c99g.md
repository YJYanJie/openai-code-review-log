# 项目名称： OpenAi 代码评审.

### 😀代码评分：90
#### 😀代码逻辑与目的：
该代码分支主要实现了动态线程池的管理功能，包括配置、查询、更新线程池配置。通过Spring Boot的配置属性和Redisson客户端，实现了线程池配置的动态调整。

#### 🤔问题点：
1. **代码重复**：`ThreadPoolConfig`类中创建了两个`ThreadPoolExecutor`实例，它们具有相同的配置，但使用了不同的Bean名称。这可能导致不必要的资源消耗。
2. **配置属性**：`application-dev.yml`中的`dynamic`配置部分被注释掉了，如果需要使用动态线程池管理功能，这部分配置需要启用。
3. **测试用例**：`AppTest`类被删除了，如果存在单元测试，应该保留以保持测试覆盖率。

#### 🎯修改建议：
1. 合并`ThreadPoolConfig`类中的两个线程池实例，只创建一个实例。
2. 启用`application-dev.yml`中的`dynamic`配置部分，以使用动态线程池管理功能。
3. 如果有单元测试，应该恢复`AppTest`类，并确保测试用例是完整的。

#### 💻修改后的代码：
```xml
<!-- dynamic-thread-pool-admin/pom.xml -->
<!-- 无需修改，仅移除了注释的依赖项 -->

<!-- dynamic-thread-pool-spring-boot-starter/pom.xml -->
<!-- 无需修改，仅移除了注释的依赖项 -->

<!-- dynamic-thread-pool-spring-boot-starter/src/main/java/cn/yj/middleware/dynamic/thread/pool/sdk/config/DynamicThreadPoolAutoConfig.java -->
<!-- 无需修改，自动配置类 -->

<!-- dynamic-thread-pool-spring-boot-starter/src/main/java/cn/yj/middleware/dynamic/thread/pool/sdk/domain/DynamicThreadPoolService.java -->
<!-- 无需修改，动态线程池服务实现 -->

<!-- dynamic-thread-pool-spring-boot-starter/src/main/java/cn/yj/middleware/dynamic/thread/pool/sdk/domain/IDynamicThreadPoolService.java -->
<!-- 无需修改，动态线程池服务接口 -->

<!-- dynamic-thread-pool-spring-boot-starter/src/main/java/cn/yj/middleware/dynamic/thread/pool/sdk/domain/model/entity/ThreadPoolConfigEntity.java -->
<!-- 无需修改，线程池配置实体对象 -->

<!-- dynamic-thread-pool-test/src/main/java/cn/yj/config/ThreadPoolConfig.java -->
```java
package cn.yj.config;

import lombok.Data;
import lombok.extern.slf4j.Slf4j;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.boot.context.properties.EnableConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.scheduling.annotation.EnableAsync;
import org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor;

import java.util.concurrent.TimeUnit;

/**
 * @Author: 1312691968@qq.com
 * @Date: 2024/10/26 21:08
 * @Description: 
 * @Version: 1.0
 */
// 使用Log4j2进行日志记录
@Slf4j
// 启用Spring的异步任务执行功能
@EnableAsync
// 定义一个配置类，并启用ThreadPoolConfigProperties配置属性
@Configuration
@EnableConfigurationProperties(ThreadPoolConfigProperties.class)
public class ThreadPoolConfig {

    /**
     * 创建并配置一个ThreadPoolExecutor实例
     * 该方法根据配置属性初始化线程池，包括线程池的核心大小、最大大小、存活时间、阻塞队列大小以及拒绝策略
     * 
     * @param properties 线程池配置属性，包含线程池的核心大小、最大大小、存活时间、阻塞队列大小和策略类型
     * @return 返回一个配置好的ThreadPoolExecutor实例
     */
    @Bean("threadPoolExecutor01")
    public ThreadPoolTaskExecutor threadPoolExecutor01(ThreadPoolConfigProperties properties) {
        // 实例化拒绝策略
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(properties.getCorePoolSize());
        executor.setMaxPoolSize(properties.getMaxPoolSize());
        executor.setKeepAliveSeconds(properties.getKeepAliveTime().intValue());
        executor.setQueueCapacity(properties.getBlockQueueSize());
        executor.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy());
        executor.initialize();
        return executor;
    }
}
```

#### 🎯修改后的配置文件：
```yaml
# dynamic-thread-pool-test/src/main/resources/application-dev.yml
dynamic:
  thread:
    pool:
      config:
        enabled: true
        host: 117.72.43.157
        port: 16379

thread:
  pool:
    executor.config:
      corePoolSize: 20
      maxPoolSize: 200
      keepAliveTime: 10s
      blockQueueSize: 5000
      policy: CallerRunsPolicy
```