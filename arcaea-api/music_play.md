# 游玩

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
        "token": songToken
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
songToken
{% endapi-method-parameter %}

{% api-method-parameter name="song\_hash" type="string" required=true %}
​铺面文件Hash值（MD5编码）
{% endapi-method-parameter %}

{% api-method-parameter name="song\_id" type="string" required=true %}
​曲目ID
{% endapi-method-parameter %}

{% api-method-parameter name="difficulty" type="number" required=true %}
​难度  
{% endapi-method-parameter %}

{% api-method-parameter name="score" type="number" required=true %}
​分数
{% endapi-method-parameter %}

{% api-method-parameter name="shiny\_perfect\_count" type="number" required=true %}
​完美Perfect数
{% endapi-method-parameter %}

{% api-method-parameter name="perfect\_count" type="number" required=true %}
​Perfect总数
{% endapi-method-parameter %}

{% api-method-parameter name="near\_count" type="number" required=true %}
​Far个数
{% endapi-method-parameter %}

{% api-method-parameter name="miss\_count" type="number" required=true %}
​Lost个数
{% endapi-method-parameter %}

{% api-method-parameter name="health" type="number" required=true %}
​回忆率（血量）
{% endapi-method-parameter %}

{% api-method-parameter name="modifier" type="number" required=true %}
挑战型 2  
其他为 1
{% endapi-method-parameter %}

{% api-method-parameter name="beyond\_gauge" type="number" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="clear\_type" type="number" required=true %}
​通关类型  
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

```javascript
{
    "success": true,
    "value": {
        "user_rating": rating
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## 排行榜

由于某些原因，616关闭了免费包曲目的世界排行榜

所以我在这里再次声明：本文档仅作学习用途，请勿滥用！否则后果自负！

{% api-method method="get" host="https://arcapi.lowiro.com" path="/latte/13/score/song/me" %}
{% api-method-summary %}
 我的排名
{% endapi-method-summary %}

{% api-method-description %}
​排行榜中条目的序号由排名高到低从0开始计数
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="song\_id" type="string" required=true %}
​曲目ID
{% endapi-method-parameter %}

{% api-method-parameter name="difficulty" type="number" required=true %}
​难度（表示方法同上传成绩中difficulty一栏）
{% endapi-method-parameter %}

{% api-method-parameter name="start" type="number" required=true %}
​玩家所在条目的序号
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=true %}
排名最低的条目的序号（​即总显示条目数 - 1）
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "success": true,
    "value": [ 成绩对象 * (limit+1) ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://arcapi.lowiro.com" path="/latte/13/score/song/friend" %}
{% api-method-summary %}
​好友
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="song\_id" type="string" required=true %}
​曲目ID
{% endapi-method-parameter %}

{% api-method-parameter name="difficulty" type="number" required=true %}
​难度
{% endapi-method-parameter %}

{% api-method-parameter name="start" type="number" required=true %}
默认为0（不知道在好友很多的时候会是什么）
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=true %}
最多显示条目数 - 1
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "success": true,
    "value": [ 成绩对象  * (limit+1) ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://arcapi.lowiro.com" path="/latte/13/score/song" %}
{% api-method-summary %}
​世界
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="song\_id" type="string" required=true %}
​曲目ID
{% endapi-method-parameter %}

{% api-method-parameter name="difficulty" type="number" required=true %}
​难度
{% endapi-method-parameter %}

{% api-method-parameter name="start" type="number" required=true %}
​默认为0（不知道如果玩家在世界榜里会是什么）
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=true %}
​最多显示条目数 - 1
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "success": true,
    "value": [ 成绩对象  * (limit+1) ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

