# Golang API Reference

此为rocketmq的api reference

## 1. message.go

### 1.1 类型概要

| 类型名称   | 类型含义                   |      |
| ---------- | -------------------------- | ---- |
| Message    | 消息类型，定义要发送的消息 |      |
| MessageExt | 消息扩展类型               |      |

### 1.2 属性概要

| 属性名称       | 类型              | 属性含义 | 所属类型 |
| -------------- | ----------------- | -------- | -------- |
| Topic          | string            | 消息主题 | Message  |
| Tags           | string            | 消息标签 | Message  |
| Keys           | string            | 业务标识 | Message  |
| Body           | string            | 消息体   | Message  |
| DelayTimeLevel | int               |          | Message  |
| Property       | map[string]string |          | Message  |

### 1.3 函数摘要

| 函数名称                 | 返回值 | 描述                   | 所属类型   |
| ------------------------ | ------ | ---------------------- | ---------- |
| String()                 |        | 输出消息内容           | Message    |
| goMsgToC(gomsg *Message) |        | golang的message转换成c | Message    |
| String()                 |        | 输出扩展消息内容       | MessageExt |

## 2. producer.go

### 2.1 类型概要

### 2.2 函数摘要

| 函数名称                                                     |       返回值       | 描述                |      |
| ------------------------------------------------------------ | :----------------: | ------------------- | ---- |
| String()                                                     |       string       | 返回配置信息        |      |
| Start()                                                      |       error        | 启动producer        |      |
| Shutdown()                                                   |       error        | 关闭producer        |      |
| SendMessageSync(msg *Message)                                | *SendResult, error | 同步发送消息        |      |
| SendMessageOrderly(msg *Message, selector MessageQueueSelector, arg interface{}, autoRetryTimes int) | *SendResult, error | 顺序发送消息        |      |
| SendMessageOneway(msg *Message)                              |       error        | oneway 方式发送消息 |      |





