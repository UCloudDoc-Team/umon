

# 回调接口

## 定义

将公网可访问到的http服务地址作为回调地址，当触发告警时，监控中心会将告警推送到该地址。

创建webhook后您的系统可以收到UCloud告警信息。当有告警时，UCloud的系统会将告警信息以HTTP
POST方式发送到指定URL，您可以对收到信息进行处理。



## 条件

用户需要提供接收POST请求的HTTP服务，以处理UCloud发送的POST请求，并将该服务的URL注册到UCloud的告警系统中。



## JSON Body Example

#### 告警

``` json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    Region: " cn-north",
    Zone: " cn-north-03",
    ResourceType: "uhost",
    ResourceId: "uhost-xxxx",
    MetricName: "MemUsage",
    AlarmTime: 1458733318,
    value: 12
    ValueUnit: %
    RecoveryTime : 0，
    Duration: 123 
    content："【UCloud】告警:北京二 2023-08-05 11:30:04 uhost(ID:uhost-xxxx-0.0.0.0-)连接数(330.00个)<6000个(优刻得公司)"
}
```

#### 恢复

``` json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    Region: " cn-north",
    Zone: " cn-north-03",
    ResourceType: "uhost",
    ResourceId: "uhost-xxxx",
    MetricName: "MemUsage",
    AlarmTime: 0,
    value: 12
    ValueUnit: %
    RecoveryTime : 1458733318，
    Duration: 123 
    content："【UCloud】告警:北京二 2023-08-05 11:30:04 uhost(ID:uhost-xxxx-0.0.0.0-)连接数(330.00个)<6000个(优刻得公司)"
}
}
```

#### 字段解释

| 字段名        | 解释说明                   |
| ------------ | ------------------------------- |
| SessionID    | 该会话的唯一标识符                |
| Region       | 地域                            |
| Zone         | 可用区                           |
| ResourceType | 资源类型                          |
| MetricName   | 指标名称                          |
| AlarmTime    | 告警触发时间                      |
| value        | 当前告警值                       |
| ValueUnit    | 单位                            |
| RecoveryTime | 告警恢复时间                     |
| Duration     | 告警持续时长，单位：秒             |
| content      | 告警内容                     |

**Response**

我们这边需要收到这样的response， 表明用户成功接收推送信息，否则会再重试2次：

``` json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    RetCode: 0
}
```

