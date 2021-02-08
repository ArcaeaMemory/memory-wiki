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

{% api-method-parameter name="difficulty" type="number" required=true %}
​难度  
PAST：0  
PRESENT：1  
FUTURE：2  
BEYOND：3
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
Fail：0  
Normal Clear：1  
Full Recall：2  
Pure Memory：3  
Easy Clear：4  
Hard Clear：5
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
排名
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

{% api-method-parameter name="start" type="string" required=true %}
​用户所在条目的序号
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="string" required=true %}
排名最低的条目的序号（​即为总显示条目 - 1）
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
    "value": [
        {
            "user_id": $UserID,
            "song_id": string, //歌曲ID
            "difficulty": 0, //难度
            "score": 1919810, //分数
            "shiny_perfect_count": 1145,//完美Perfect数
            "perfect_count": 1413, //Perfect总数
            "near_count": 11, //Far数量
            "miss_count": 45, //Miss数量
            "health": 100, //回忆率（血量）
            "modifier": 0, //游玩模式（同上文中提到的modifier）
            "time_played": 1608383064657, //游玩时间
            "best_clear_type": 5, //最高的通关类型（从低到高排序为4<1<5<2<3）
            "clear_type": 1, //通关类型
            "name": string, //用户名
            "character": 24, //搭档
            "is_skill_sealed": false, //技能是否被锁定
            "is_char_uncapped": false, //搭档是否已觉醒
            "rank": 7764 //排名
        } *(limit+1)
    ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

