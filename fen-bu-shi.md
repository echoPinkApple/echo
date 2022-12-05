---
description: 分布式学习笔记
---

# 分布式

### nginx作用：

动态资源和静态资源分离；网关作用：做统一认证，鉴权，限流等操作；

nginx请求转发默认丢弃host等信息，通过proxy\_set\_header添加请求头：proxy\_setHeader Host $host

### RabbitMQ:

#### 重要注解：

@RabbitListener:标注在方法上，用来表示需要监听哪些队列

@RabbitHandler:标注在方法上，用来重载监听方法。

#### RabbitMQ消息确认机制-可靠抵达：

#### RabbitMQ 延迟队列：

消息的TTL：消息的存活时间；

死信：一个消息被consumer拒收，或消息ttl到期还没被消费，队列长度满了，排在前面的消息被丢弃；

### 服务调用链路追踪：

#### sleuth+zipkin：

sleuth：链路追踪；zipkin：链路追踪可视化界面

高并发关键：缓存，异步，队列。



### kubernates：



