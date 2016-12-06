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
| app_token    |  String    |是   | 用于验证app身份，默认值为："xxx"，应用每次后台上传数据必须携带此token      |
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

