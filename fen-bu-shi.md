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

