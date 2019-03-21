# Golang API Reference

此为rocketmq的api reference

## 1. api.go

### 1. struct(结构)概要

| struct（结构）     | 备注                         |      |
| ------------------ | ---------------------------- | ---- |
| ClientConfig       | 客户端配置                   |      |
| ProducerConfig     | 消息生产者配置               |      |
| PushConsumerConfig | 消费者配置(Borker主动推送)   |      |
| PullConsumerConfig | 消费者配置(Consumer主动拉取) |      |

### 2. 属性概要

| 属性名称            | 类型                | 含义                    | 所属struct(结构)   |
| ------------------- | ------------------- | ----------------------- | ------------------ |
| GroupID             | string              | 分组ID                  | ClientConfig       |
| NameServer          | string              | 命名服务地址            | ClientConfig       |
| NameServerDomain    | string              | 命名服务(HTTP Endpoint) | ClientConfig       |
| GroupName           | string              | 分组名称                | ClientConfig       |
| InstanceName        | string              | 实例名称                | ClientConfig       |
| Credentials         | *SessionCredentials | 安全认证配置            | ClientConfig       |
| LogC                | *LogConfig          | 日志配置                | ClientConfig       |
|                     |                     |                         |                    |
| ClientConfig        |                     | 客户端配置              | ProducerConfig     |
| SendMsgTimeout      | int                 | 消息发送超时时间        | ProducerConfig     |
| CompressLevel       | int                 | 压缩级别                | ProducerConfig     |
| MaxMessageSize      | int                 | 最大消息量              | ProducerConfig     |
|                     |                     |                         |                    |
| ClientConfig        |                     | 客户端配置              | PushConsumerConfig |
| ThreadCount         | int                 | 线程数量                | PushConsumerConfig |
| MessageBatchMaxSize | int                 | 批量消费的最大消息条数  | PushConsumerConfig |
| Model               | MessageModel        | 消息模型(广播or集群)    | PushConsumerConfig |
|                     |                     |                         |                    |
| ClientConfig        |                     | 客户端配置              | PullConsumerConfig |

### 1.3 函数概要



## 2. message.go

### 2.1 struct(结构)概要

| struct（结构） | 备注     |      |
| -------------- | -------- | ---- |
| Message        | 消息     |      |
| MessageExt     | 消息扩展 |      |

### 2.2 属性概要

| 属性名称       | 类型              | 属性含义 | 所属struct(结构) |
| -------------- | ----------------- | -------- | ---------------- |
| Topic          | string            | 消息主题 | Message          |
| Tags           | string            | 消息标签 | Message          |
| Keys           | string            | 业务标识 | Message          |
| Body           | string            | 消息体   | Message          |
| DelayTimeLevel | int               |          | Message          |
| Property       | map[string]string |          | Message          |

### 2.3 函数摘要

| 函数名称                 | 返回值 | 描述                   | 所属struct(结构) |
| ------------------------ | ------ | ---------------------- | ---------------- |
| String()                 |        | 输出消息内容           | Message          |
| goMsgToC(gomsg *Message) |        | golang的message转换成c | Message          |
| String()                 |        | 输出扩展消息内容       | MessageExt       |

## 3. producer.go

### 3.1 struct(结构)概要

| struct（结构）  | 含义           |      |
| --------------- | -------------- | ---- |
| defaultProducer | 默认消息生产者 |      |

### 3.2 属性摘要

| 属性     | 类型                | 含义               | 所属struct(构造) |
| -------- | ------------------- | ------------------ | ---------------- |
| config   | *ProducerConfig     | 消息生产者配置信息 | defaultProducer  |
| cproduer | *C.struct_CProducer | 对应C的消息生产者  | defaultProducer  |
|          |                     |                    |                  |



### 3.3 函数摘要

| 函数名称                                                     |       返回值       | 描述                |      |
| ------------------------------------------------------------ | :----------------: | ------------------- | ---- |
| String()                                                     |       string       | 返回配置信息        |      |
| Start()                                                      |       error        | 启动producer        |      |
| Shutdown()                                                   |       error        | 关闭producer        |      |
| SendMessageSync(msg *Message)                                | *SendResult, error | 同步发送消息        |      |
| SendMessageOrderly(msg *Message, selector MessageQueueSelector, arg interface{}, autoRetryTimes int) | *SendResult, error | 顺序发送消息        |      |
| SendMessageOneway(msg *Message)                              |       error        | oneway 方式发送消息 |      |
