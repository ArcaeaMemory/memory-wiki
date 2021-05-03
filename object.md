# 术语

## 难度

```
0：PAST 
1：PRESENT  
2：FUTURE  
3：BEYOND
```

## 通关类型

```
0：Fail
1：Normal Clear
2：Full Recall
3：Pure Memory 
4：Easy Clear 
5：Hard Clear
```

# 对象

## 成绩对象

```javascript
{
    "user_id": 玩家ID,
    "song_id": 歌曲ID,
    "difficulty": 难度,
    "score": 分数,
    "shiny_perfect_count": 完美Perfect数,
    "perfect_count": Perfect总数,
    "near_count": Far数量,
    "miss_count": Miss数量,
    "health": 回忆率（血量）,
    "modifier": 游玩模式,
    "time_played": 游玩时间,
    "best_clear_type": 最高的通关类型（从低到高排序为4<1<5<2<3）,
    "clear_type": 通关类型,
    "name": 用户名,
    "character": 搭档,
    "is_skill_sealed": 技能是否被锁定,
    "is_char_uncapped": 搭档是否已觉醒,
    "rank": 排名
}
```