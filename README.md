# 数据规范及接口文档定义

标签（空格分隔）： api

---

## 1. 用户信息模块
### 1.1 用户信息获取
客户端请求url: http://ip:8082/kcmim/api/userinfo
请求方式：get
参数：userId(用户id)
| 参数名称      |    数据类型  |是否必须 |描述|
| :-------- | :--------     |:------| :-----------------|
| userId    |  String    |是   | 标识用户的id      |

返回json格式：
```
{
    "loginId": "123456", 
    "username": "系统管理员", 
    "userId": "xxx", 
    "roleIds": null, 
    "nickname": "Clarence", 
    "bornDate": "1998-10-01", 
    "sex": "男", 
    "employeeState": "在职", 
    "phoneNumber": "15678350023", 
    "email": "zjianhao@qq.com"
}
```

实体类定义：
```

package com.szk.model;

/**
 * Created by 张建浩（Clarence) on 2016-10-26 23:10.
 * the author's website:http://www.zjianhao.cn
 * the author's github: https://github.com/zhangjianhao
 * contact: zhangjianhao1111@gmail.com
 */

public class User {
    private String loginId;
    private String username;
    private String userId;
    private String roleIds;

    private String nickname;
    private String bornDate;
    private String sex;//性别
    private String employeeState;
    private String phoneNumber;
    private String email;

    public String getNickname() {
        return nickname;
    }

    public void setNickname(String nickname) {
        this.nickname = nickname;
    }

    public String getBornDate() {
        return bornDate;
    }

    public void setBornDate(String bornDate) {
        this.bornDate = bornDate;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public String getEmployeeState() {
        return employeeState;
    }

    public void setEmployeeState(String employeeState) {
        this.employeeState = employeeState;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getLoginId() {
        return loginId;
    }

    public void setLoginId(String loginId) {
        this.loginId = loginId;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getUserId() {
        return userId;
    }

    public void setUserId(String userId) {
        this.userId = userId;
    }

    public String getRoleIds() {
        return roleIds;
    }

    public void setRoleIds(String roleIds) {
        this.roleIds = roleIds;
    }
}

```


### 1.2 用户信息修改
客户端请求url: http://ip:8082/kcmim/api/userupdate
请求方式：POST
请求参数：
| 参数名称      |    数据类型  |是否必须 |描述|
| :-------- | :--------     |:------| :-----------------|
| userId    |  String       |   是|标识用户的id ,此处用来查找用户，不用于修改     |
| username  |  String       | 否| 用户昵称          |
| borndate  |  String       | 否|出生日期          |
| sex       |  String       | 否|性别              |
| borndate  |  String       | 否|出生日期          |
| phone_number  |  String      |否 | 电话号码          |
| email  |  String       |否 | 邮箱        |

    
返回数据：
```
{"code":"1","desc":"错误描述信息"}
```
> 返回数据说明：
code = 1 表明数据修改成功
code < 0 修改失败
desc: 错误描述信息


### 1.3用户设置

客户端请求url: http://ip:8082/kcmim/api/userupdate
请求方式：POST
请求参数：
| 参数名称      |    数据类型  |是否必须 |描述|
| :-------- | :--------     |:------| :-----------------|
| userId    |  String       |   是|标识用户的id ,此处用来查找用户，不用于修改     |
| sms_notification  |  Boolean       | 否| 是否开启短信提醒          |
| email_notification  |  Boolean       | 否|是否开启邮箱提醒          |

返回数据：
```
{"code":"1","desc":"错误描述信息"}
```
> 返回数据说明：
code = 1 表明设置成功
code < 0 设置失败
desc: 错误描述信息

## 2.事件统计
功能说明：统计当前登陆用户的总事件数量，今天总产生事件数量，已处理事件数量
客户端请求url: http://ip:8082/kcmim/api/event_statistics
请求方式：get
请求参数：
| 参数名称      |    数据类型  |是否必须 |描述|
| :-------- | :--------     |:------| :-----------------|
| userId    |  String       |   是|标识用户的id ,此处用来查找用户，不用于修改     |


返回json数据示例
```
{
    "event_total": "123", 
    "event_today": "5", 
    "solved_event": "2"
}
```
> 返回数据说明：
event_total:当前登陆用户的总事件数量
event_today:今天总产生时间数量
solved_event:已处理事件数量

## 3 登陆模块

### 3.1 验证码获取
客户端请求url: http://ip:8082/kcmim/api/verify_code
请求方式：POST
请求参数：
| 参数名称      |    数据类型  |是否必须 |描述|
| :-------- | :--------     |:------| :-----------------|
| account    |  String       |   是| 登陆账户名,此处可以是账户名，手机，邮箱。服务端根据账户名查询用户手机号码，并发送验证码    |

返回数据
```
{
    ”code","200",
    "desc":"xxx"
}
```
> 返回数据说明：
code 200 发送验证码成功
code < 0 验证码发送失败
desc 错误描述

### 3.2 登陆验证

客户端请求url: http://ip:8082/kcmim/api/login
请求方式：POST
请求参数：
| 参数名称      |    数据类型  |是否必须 |描述|
| :-------- | :--------     |:------| :-----------------|
| account    |  String       |   是| 用户账户（此处可以是账户名，手机，邮箱）     |
| password  | String | 是| 账户密码|
|verify_code| String | 是| 用户手机接收到的验证码|


返回json数据示例
```
{
    “code","200"
    "desc","登陆成功"
    "loginId","xxx",
    "userName","xxx",
    "userId","xxx",
    "roleIds","xxx"
}
```
> 返回数据说明：
code 200 发送验证码成功
code < 0 登陆验证失败
desc 描述验证失败原因，包括用户不存在，密码错误，验证码错误等







