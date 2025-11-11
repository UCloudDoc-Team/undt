# 回调告警内容说明

网络拨测支持将探测任务产生的告警信息推送至指定通知组设置的回调地址。

## 回调地址配置

在[资源监控-通知人管理](https://console.ucloud.cn/umon/contact)，创建新的通知组或编辑已有的通知组，通知方式勾选“回调接口”，填写需要推送告警信息的回调地址（公网可访问到的URL）。

![配置回调地址](images/配置回调地址.PNG)

## 请求参数说明

### 告警信息

```json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    ResourceType: "UNDT",
    ResourceId: "xxxxxxxxxxxxxxxxxxxxxxx",
    MetricName: "Lost",
    AlarmTime: 1458733318,
    RecoveryTime : 0,
    Content:"网络拨测监控发生告警，探测任务:回调测试3(bwdcmkq8wyryy)，探测地址:8.8.8.8，
告警等级P0，告警类型:首次告警，告警内容:【P0】电信-上海-上海 到 8.8.8.8当前丢包:100%阈值:50%"
}
```

### 恢复信息

```json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    ResourceType: "UNDT",
    ResourceId: "xxxxxxxxxxxxxxxxxxxxxxx",
    MetricName: "Lost",
    AlarmTime: 0,
    RecoveryTime :  1458733318,
    Content:"网络拨测告警恢复，探测任务:“回调测试3(bwdcmkq8wyryy)”，探测地址:8.8.8.8，
告警内容:电信-上海-上海 到 8.8.8.8当前丢包:0%，告警已恢复"
}
```

## 字段说明

| 字段         | 字段类型 | 说明                                     |
| :----------- | :------- | :--------------------------------------- |
| SessionID    | string   | 该会话的唯一标识符                       |
| ResourceType | string   | UNDT:网络拨测（UCloud Network DialTest） |
| ResourceId   | string   | 拨测任务ID                               |
| MetricName   | string   | 指标名称。Lost：丢包率； Rtt：时延。     |
| AlarmTime    | int64    | 告警时间                                 |
| RecoveryTime | int64    | 恢复时间                                 |
| Content      | string   | 告警内容                                 |

## Response

我们这边需要收到这样的response， 表明用户成功接收推送信息，否则会再重试2次：

```json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    RetCode: 0
}
```

