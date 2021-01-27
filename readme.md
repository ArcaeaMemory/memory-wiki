# 必读

## 变量

 该API文档为方便理解，会使用变量以及简写编码转换（~~其实就是懒~~

> 变量格式：$变量名
>
> 编码转换：$编码格式\(原文本\)

变量说明：

* AppVersion：Arcaea版本
* Name：账户用户名
* Password：账户密码
* Email：账户邮箱
* DeviceID：设备ID（移动端设备标识码之一）
* Platform：设备平台（android或ios）
* UserID：用户ID
* AccessToken：登录令牌（注册或登录后获取）

如无特殊说明，所有的请求中Header一定包含以下内容：

|  |  |
| :--- | :--- |
| Accept-Encoding | identity |
| Content-Type | application/x-www-form-urlencoded; charset=utf-8 |
| AppVersion | $AppVersion |



