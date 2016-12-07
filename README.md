# 数据规范及接口文档定义

标签（空格分隔）： api

---

## 1. 学习记录数据上传

客户端请求url: http://ip:80/pscstudy/api/user/study_records

请求方式：post

参数列表

| 参数名称      |    数据类型  |是否必须 |描述|
| :-------- | :--------     |:------| :-----------------|
| deviceId    |  String    |是   | 设备的id,用于区分用户      |
| appId    |  String    |是   | 应用包名，用于区分上传数据的app身份，本应用使用com.guet.pscstudy作为appId      |
| app_token    |  String    |是   | 用于验证app身份，默认值为："907411cf-18b9-4fd6-8810-316e4e2f1370"，应用每次后台上传数据必须携带此token      |
| data    |  String(Json)    |否   | 学习记录数据     |

data json 数据格式,如：

```
[
    {
        "date": "1481039299361",
        "week": 1,
        "studyTime": 80
    },
    {
        "date": "1481039299361",
        "week": 2,
        "studyTime": 60
    }
]
```
>date 为long类型的日期，week为对应的周数，studyTime为该日期学习的总时长，单位为min

返回数据格式：
```
{
   "code":"200",
   "desc":"数据保存成功"
}
```
> code < 0 表示失败，desc加失败原因


## 2. 错误字词上传

客户端请求url: http://ip:80/pscstudy/api/user/error_records

请求方式：post

参数列表

| 参数名称      |    数据类型  |是否必须 |描述|
| :-------- | :--------     |:------| :-----------------|
| deviceId    |  String    |是   | 设备的id,用于区分用户      |
| appId    |  String    |是   | 应用包名，用于区分上传数据的app身份，本应用使用com.guet.pscstudy作为appId      |
| app_token    |  String    |是   | 用于验证app身份，默认值为："907411cf-18b9-4fd6-8810-316e4e2f1370"，应用每次后台上传数据必须携带此token      |
| errors    |  String(Json)    |否   | 错误记录数据     |
> 注意：客户端在用户测评完给出统计结果后，将测评中的错误字词上传。该字词可能在服务端已经存在，对于存在的字词，服务端存储时应更新其错误次数，避免同一错误字词多次存储

errors字段 json 数据格式,如：

```
[
    {
        "word": "测试",
        "rightPronunciation": "ce4shi4",
        "errorType": "漏读",
        "errorTime": "1481122198043",
        "frequency": 2
    },
    {
        "word": "发",
        "rightPronunciation": "fa1",
        "errorType": "回读",
        "errorTime": "1481122198043",
        "frequency": 1
    }
]
```
> word 错误字词，rightPronunciation 正确发音，errorType错误类型，errorTime 错误时间（最近一次错误时间)，frequency 错误次数

返回数据格式：

```
{
   "code":"200",
   "desc":"数据保存成功"
}
```
> code < 0 表示失败，desc加失败原因
