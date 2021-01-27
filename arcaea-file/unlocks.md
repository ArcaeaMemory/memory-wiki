# 解锁条件\(unlocks\)格式

## 总论

文件在\assets\songs下

打开文件大概是这样的画风：

```javascript
{
 "unlocks": [
   {
     "songId": …,
     "ratingClass": …,
     "conditions": [
       …
       ],
       …
   },
   …
 ]
}
```

整个文件以一个大括号和一个”unlocks”字符串开头，大体结构如下

```javascript
{
  "unlocks":[
  //all contents…
  ]
}
```

## 细节解析

例子

```javascript
{
     "songId": "chronostasis",
     "ratingClass": 1,
     "conditions": [
       {
         "type": 1,
         "song_id": "infinityheaven",
         "song_difficulty": 1,
         "grade": 0
       },
       {
         "type": 0,
         "credit": 80
       }
     ]
}
```

归纳

```javascript
{
  "songId": this.songname,
  "ratingClass": classNum,
  "conditions": [
    {
     //condition 1
    },
    {
     //condition 2
    }
 ]  //end of condition(s)
}
```

从上到下依次解析如下：

* songId \(String）：双引号包含的字符串，代表了欲限定条件的歌曲名称。**至关重要**，所引用歌曲对应谱面文件夹也必须是id名，不能出现非ASCII字符
* ratingClass \(int\)：代表了欲限定条件的歌曲难度，取值只能为0，1，2。0为PST难度，1为PRS难度，2为FTR难度。
* conditions：unlocks文件中的核心，以一对英文方括号包裹，每一个condition语句组以一对大括号包含。一个歌曲的一个难度可以有很多个condition语句组，它们之间以英文逗号分开。

每一个语句组中一定有一个type语句，根据type的取值不同，其中会有不同的呈现。

#### **残片型解锁**

```javascript
{
   "type": 0,
   "credit": frag_needed_to_unlock
}
```

当type取0时，为残片型解锁。玩家需要花费残片来开启当前歌曲的游玩权限。credit的取值是一个整数，代表了解锁当前难度歌曲需要花费的残片数量。

#### 先行通过歌曲型解锁

```javascript
{
    "type":1,    
    "song_id": songname,
    "song_difficulty": difficulty,
    "grade": gradeNum
}
```

type取1时，为先行通过歌曲型解锁，玩家需要在其前置歌曲中达到相应要求。

* song\_id \(String\)：指在游玩本难度的歌曲时，需要先行通过的歌曲名称，引用要求与songId相同。
* song\_difficulty \(int\)：取值为0，1，2，与ratingClass含义相同。
* grade \(int\)：限定先行通过的歌曲需要达到的评级，0为不限定，1为达到C，2为达到B，3为达到A，4为达到AA，5为达到EX。

#### **先**行游玩歌曲型解锁

```javascript
{
    "type":2,    
    "song_id": songname,
    "song_difficulty": difficulty
}
```

 type取2时，为先行游玩歌曲型解锁，与[先行通过歌曲型解锁](https://arcaeamemory.gitbook.io/memory-wiki/arcaea-file/unlocks#先行通过歌曲型解锁)类似，不过对应结果为游玩相应曲目即可。变量不再赘述。

#### 多次通过歌曲型解锁

```javascript
{
    "type":3,    
    "song_id": songname,
    "song_difficulty": difficulty,
    "grade": gradeNum,
    "times": timesNum
}
```

type取3时，为多次通过歌曲型解锁，与[先行通过歌曲型解锁](https://wiki.arcaea.cn/index.php/%E8%A7%A3%E9%94%81%E6%9D%A1%E4%BB%B6%28unlocks%29%E6%A0%BC%E5%BC%8F#.E5.85.88.E8.A1.8C.E9.80.9A.E8.BF.87.E6.AD.8C.E6.9B.B2.E5.9E.8B.E8.A7.A3.E9.94.81)类似，不过需要多次通过相应曲目并达到给定评级。

* times \(int\)：指先行通过的歌曲需要达到限定评级的次数。

其他变量不再赘述。

#### **选择任务型解锁**

```javascript
{
    "type":4,
    "conditions": [
    {
     //condition 1
    },
    {
     //condition 2
    }
 ]  //end of condition(s)
}
```

type取4时，为选择任务型解锁。其中conditions类似最外侧的conditions，可填入不同的condition语句组。玩家只需挑选其中任意一个任务完成即可解锁。~~套娃警告~~

#### **个人游玩潜力值型解锁**

```javascript
{
    "type":5,    
    "rating": potentialNum
}
```

type取5时，为个人游玩潜力值型解锁，玩家需要取得或超过限定的潜力值即可解锁。

* rating \(int\)：指限定的个人游玩潜力值乘以100后的整数。可以随便填，负数都行

#### **特殊解锁类型**

```jsx
{
   "type": 101,
   "min": minNum,
   "max": maxNum
}
```

type取101时，为特殊解锁类型，通常用于解锁隐藏歌曲。

* min \(int\)：解锁anomaly失败时获得的最小进度数。
* max \(int\)：解锁anomaly失败时获得的最大进度数。

