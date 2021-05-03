# 账户

{% api-method method="post" host="https://arcapi.lowiro.com" path="/latte/13/user/" %}
{% api-method-summary %}
注册
{% endapi-method-summary %}

{% api-method-description %}
​由于条件有限，本条目不保证正确
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="name" type="string" required=true %}
用户名
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
密码
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
电子邮箱
{% endapi-method-parameter %}

{% api-method-parameter name="platform" type="string" required=true %}
操作系统
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "access_token": 登录凭证,
    "token_type": "Bearer",
    "success": true
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://arcapi.lowiro.com" path="/latte/13/auth/login" %}
{% api-method-summary %}
登录
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic $base64\($Name:$Password\)
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="grant\_type" type="string" required=true %}
client\_credentials
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
登录成功
{% endapi-method-response-example-description %}

```javascript
{
    "access_token": 登录凭证,
    "token_type": "Bearer",
    "success": true
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}

超过两台设备登录

{% endapi-method-response-example-description %}

```
{
    "success": false,
    "error_code": 105,
    "extra": {
        "remaining_ts": 时间/秒
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}
的
{% endapi-method-response-example-description %}

```javascript
{
    "success": false,
    "error_code": 104
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

