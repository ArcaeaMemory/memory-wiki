# 账户

{% api-method method="post" host="https://arcapi.lowiro.com" path="/coffee/12/user/" %}
{% api-method-summary %}
注册
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Accept-Encoding" type="string" required=true %}
identity
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
application/x-www-form-urlencoded; charset=utf-8
{% endapi-method-parameter %}

{% api-method-parameter name="AppVersion" type="string" required=true %}
$AppVersion
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="name" type="string" required=true %}
$Name
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
$Password
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
$Email
{% endapi-method-parameter %}

{% api-method-parameter name="device\_id" type="string" required=true %}
$DeviceID
{% endapi-method-parameter %}

{% api-method-parameter name="platform" type="string" required=true %}
$Platform
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "success": true,
    "value": {
        "user_id": $UserID,
        "access_token": $AccessToken
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

