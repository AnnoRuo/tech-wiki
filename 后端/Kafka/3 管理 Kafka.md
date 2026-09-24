
## AdminClient 概述

Kafka AdminClient 是 Apache Kafka 提供的一个管理客户端 API，用来以编程方式管理和监控 Kafka 集群资源（例如，主题、分区、Broker）。该 API 的特性是：
- 异步：所有操作的结果都是基于 Future 封装的异步对象
- 最终一致性：集群中的控制器接收到 API 所发送过来的请求后，在本地处理完元数据变更，便直接向客户端返回结果了，并不会阻塞等待其他 Broker 同步完元数据。

所有修改集群状态的操作（创建、删除和变更）均由控制器处理。而读取集群状态的操作会基于客户端所知信息被路由到当前负载最低的代理。


## AdminClient 生命周期

```java
Properties props = new Properties();
// 建议至少指定三个代理，防止某个代理不可用
props.put(AdminClientConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");

AdminClient client = AdminClient.create(props);
client.close();
```


`close()`：如果未指定超时时间，那么就等待所有操作执行完成。否则，如果超出了指定时间，那么将中止所有正在进行中的操作并抛出超时异常。


## 配置

- `client.dns.lookup`：
- `request.timeout.ms`：

## 主题管理

## 配置管理

## 消费者组管理

## 集群元数据

## 高级管理操作

## 测试