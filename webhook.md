

# 回调接口

## 定义

回调是一种告警通知方式，当监控系统检测到满足触发条件的告警事件时，会通过用户配置的回调URL向用户系统发送告警信息。
 回调由云监控主动发起，通常使用 **HTTP/HTTPS POST** 请求，将告警事件的详细信息（如告警名称、触发时间、资源信息、当前指标值等）以结构化数据（如 JSON）推送到用户的接收端。

## 条件

1. **提供可公网访问的回调地址**
   - 云监控会通过公网访问用户配置的回调 URL，必须保证该地址能被外部正常访问。
2. **支持指定的协议与方法**
   - 回调请求通常使用 `HTTP` 或 `HTTPS` 协议。
   - 云监控默认使用 **POST** 方法推送数据，用户的接收服务需要支持并正确解析请求体。

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
    value: 12,
    ValueUnit: %,
    RecoveryTime : 0，
    Duration: 123 ,
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
    value: 12,
    ValueUnit: %,
    RecoveryTime : 1458733318，
    Duration: 123,
    content："【UCloud】告警恢复:北京二 2023-08-05 11:30:04 uhost(ID:uhost-xxxx-0.0.0.0-)连接数(330.00个)<6000个(优刻得公司)"
}
```

#### 字段解释

| 字段名        | 解释说明                   |
| ------------ | ------------------------------- |
| SessionID    | 该会话的唯一标识符                |
| Region       | 地域                            |
| Zone         | 可用区                           |
| ResourceType | 资源类型                          |
| ResourceId | 资源ID |
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

