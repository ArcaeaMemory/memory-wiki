# 成绩

## 上传

{% api-method method="get" host="https://arcapi.lowiro.com" path="/latte/13/score/token" %}
{% api-method-summary %}
 获取token
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "success": true,
    "value": {
        "token": $SongToken
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://arcapi.lowiro.com" path="/latte/13/score/song" %}
{% api-method-summary %}
​上传成绩
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="song\_token" type="string" required=true %}
$SongToken
{% endapi-method-parameter %}

{% api-method-parameter name="song\_hash" type="string" required=true %}
​铺面文件Hash值（MD5编码）
{% endapi-method-parameter %}

{% api-method-parameter name="song\_id" type="string" required=true %}
​曲目ID
{% endapi-method-parameter %}

{% api-method-parameter name="difficulty" type="string" required=true %}
​难度  
PAST：0  
PRESENT：1  
FUTURE：2  
BEYOND：3
{% endapi-method-parameter %}

{% api-method-parameter name="score" type="string" required=true %}
​分数
{% endapi-method-parameter %}

{% api-method-parameter name="shiny\_perfect\_count" type="string" required=true %}
​完美Perfect数
{% endapi-method-parameter %}

{% api-method-parameter name="perfect\_count" type="string" required=true %}
​Perfect总数
{% endapi-method-parameter %}

{% api-method-parameter name="near\_count" type="string" required=true %}
​Far个数
{% endapi-method-parameter %}

{% api-method-parameter name="miss\_count" type="string" required=true %}
​Lost个数
{% endapi-method-parameter %}

{% api-method-parameter name="health" type="string" required=true %}
​回忆率（血量）
{% endapi-method-parameter %}

{% api-method-parameter name="modifier" type="string" required=true %}
挑战型 2  
其他为 1
{% endapi-method-parameter %}

{% api-method-parameter name="beyond\_gauge" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="clear\_type" type="string" required=true %}
​通关类型  
失败：0  
平衡型：1  
支援型（骨折光也是）：4  
挑战型：5
{% endapi-method-parameter %}

{% api-method-parameter name="submission\_hash" type="string" required=true %}
​MD5\(song\_token  + song\_hash + song\_id + difficulty + score + shiny\_perfect\_count + perfect\_count+ near\_count + miss\_count + health + modifier + clear\_type + MD5\($UserID + song\_hash\)\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

