

# 回调接口

## 定义

将公网可访问到的http服务地址作为回调地址，当触发告警时，监控中心会将告警推送到该地址。

创建webhook后您的系统可以收到UCloud告警信息。当有告警时，UCloud的系统会将告警信息以HTTP
POST方式发送到指定URL，您可以对收到信息进行处理。



## 条件

用户需要提供接收POST请求的HTTP服务，以处理UCloud发送的POST请求，并将该服务的URL注册到UCloud的告警系统中。



## JSON Body Example

#### 告警

```json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    Region: " cn-north-03",
    ResourceType: "uhost",
    ResourceId: "uhost-xxxx",
    MetricName: "MemUsage",
    AlarmTime: 1458733318,
    RecoveryTime : 0
}
```

#### 恢复

```json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    Region: "cn-north-03",
    ResourceType: "uhost",
    ResourceId: "uhost-xxxx",
    MetricName: "MemUsage",
    AlarmTime: 0,
    RecoveryTime: 1458733318
}
```

#### Field Explaination

| Field        | Explaination                    |
| ------------ | ------------------------------- |
| SessionID    | Session ID for this message     |
| Region       | Region Name                     |
| ResourceType | Resource Type                   |
| MetricName   | Metric Name for current warning |
| AlarmTime    | Alarm time                      |
| RecoveryTime | Restory time                    |
| Content      | Warning content                 |

**Response**

我们这边需要收到这样的response， 表明用户成功接收推送信息，否则会再重试2次：

```json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    RetCode: 0
}
```

