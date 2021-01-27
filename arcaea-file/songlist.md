# 歌曲信息\(songlist\)格式

## 在开始阅读之前

### 总论

本文件是关于更改歌曲信息的,如果想更改谱面本身,请移步[谱面格式](https://arcaeamemory.gitbook.io/memory-wiki/arcaea-file/aff)

如果想更改关于解歌条件的部分,请移步[解锁条件\(unlocks\)格式](https://wiki.arcaea.cn/index.php/%E8%A7%A3%E9%94%81%E6%9D%A1%E4%BB%B6%28unlocks%29%E6%A0%BC%E5%BC%8F)

如果想更改曲包相关内容请移步[曲包信息\(packlist\)格式](https://wiki.arcaea.cn/index.php/%E6%9B%B2%E5%8C%85%E4%BF%A1%E6%81%AF%28packlist%29%E6%A0%BC%E5%BC%8F)

### 阅读总论

本文件名为songlist，包含了除教程及愚人节外的全部歌曲相关信息。

本文件在安卓apk安装包里的位置为 \assets\songs\songlist，在苹果ipa安装包内位置为 \Payload\Arc-mobile.app\songs\songlist

本文件为json文档，有大量花括号与中括号，格式要求较为严格，最后一个字段后不能出现多余的逗号。本文件用两空格缩进整理版面。

**任何对本文件的修改都会导致游戏程序崩溃，这是因为程序中对本文件有哈希校验。**

**从这里开始就会涉及到危险操作了,请为自己的行为负责!**

## 代码解析

### 框架

本文件总体框架如下。每一首歌曲的信息互不干扰。

```javascript
{
  "songs": [
    {
      // song 1
    },
    {
      // song 2
    } ...
  ]
}
```

### 细节解析

* 数据格式：
  * string -- 字符串 例："brandnewworld"
  * int -- 整数 例：54401
  * boolean -- 布朗值 例：true（是）, false（否）
* localized字段可选属性：
  * "en" -- 英文 **默认语言**
  * "ja" -- 日文
  * "ko" -- 韩文
  * "zh-Hans" -- 简体中文
  * "zh-Hant" -- 繁体中文

以下为歌曲信息最完整的格式

```javascript
{
  "id": string (ASCII),
  "title_localized": {
    "en": string ...
  },
  "artist": string,
  "artist_localized": {
    "en": string ...
  },
  "bpm": string,
  "bpm_base": int,
  "set": string,
  "purchase": string,
  "audioPreview": int,
  "audioPreviewEnd": int,
  "side": int (0, 1),
  "bg": string (ASCII),
  "bg_daynight": {
      "day": string (ASCII),
      "night": string (ASCII)
  },
  "date": int (timestamp),
  "version": string,
  "world_unlock": boolean,
  "remote_dl": boolean,
  "byd_local_unlock": boolean,
  "songlist_hidden": boolean,
  "no_pp": boolean,
  "source_localized": {
    "en": string ...
  },
  "source_copyright": string,
   "no_stream": boolean,
  "jacket_localized": {
    "ja": boolean ...
  },
  "difficulties": [
    {
      "ratingClass": int (0, 1, 2, 3),
      "chartDesigner": string,
      "jacketDesigner": string,
      "rating": int,
      "ratingPlus": boolean,
      "plusFingers": boolean,
      "jacket_night": string (ASCII),
      "jacketOverride": boolean,
      "hidden_until_unlocked": boolean,
      "bg": string (ASCII),
      "world_unlock": boolean
    } ...
  ]
}
```

#### 歌曲信息

 注：以下**必需字段**指官方songlist文件中每首歌都有的字段，删除后是否会导致游戏崩溃并未经测试。

```javascript
{
  "id": string (ASCII),
    // 游戏程序识别歌曲的唯一ID 只能使用ASCII字符 必需字段
  
  "title_localized": {
    "en": string,
    "ja": string ...
  },
    // 游戏内显示的曲名，可分语言设定 必需字段
  
  "artist": string,
  "artist_localized": {
    "en": string ...
  },// 游戏内显示的作曲者，可分语言设定。可只填artist，默认为英语 必需字段

  "bpm": string,
    // 游戏内显示的BPM 必需字段

  "bpm_base": int,
    // 基准BPM，实际游玩速度为设置的音符流速除以"bpm_base"再乘以谱面bpm 必需字段
  
  "set": string,
    // 本曲所属曲包名，参考曲包信息(packlist)格式 必需字段
  
  "purchase": string,
    // 本曲购买方式，曲包曲填所属曲包名，单曲填本曲"id"，无需购买则留空 必需字段
  
  "audioPreview": int,
  "audioPreviewEnd": int,
    // 本曲预览的开始与结束时间，单位为毫秒 必需字段
  
  "side": int (0, 1),
    // 本曲属性，0为光侧，1为对立侧 必需字段
  
  "bg": string (ASCII),
    // 本曲背景名，背景jpg储存在\assets\img\bg目录中，留空即为默认背景 只能使用ASCII字符 必需字段
  
  "bg_daynight": {
      "day": string (ASCII),
      "night": string (ASCII)
  },// 自定义白天及夜晚显示的不同背景，参考 群愿 的技能 只能使用ASCII字符
  
  "date": int (timestamp),
    // 本曲加入时刻的10位时间戳 必需字段
  
  "version": string,
    // 本曲加入时的游戏版本，用于歌曲分类 必需字段
  
  "world_unlock": boolean,
    // 本曲是否需要世界模式解锁
  
  "remote_dl": boolean,
    // 本曲是否需要从服务器下载
  
  "byd_local_unlock": boolean,
    // 本曲Beyond难度是否在本地解锁。应与"world_unlock"相反 
  
  "songlist_hidden": boolean,
    // 本曲解锁前是否歌曲界面中隐藏 
  
  "no_pp": boolean,
    // 标记lowiro是否拥有本曲的版权。本字段对游戏没有影响
  
  "source_localized": {
    "en": string ...
  },// 本曲出处，可分语言设定。歌曲界面中选择歌曲后，歌曲下方会显示 from 「"source_localized"」（其他语言）/《》（中文）
  
  "source_copyright": string,
    // 本曲版权方，仅当"source_localized"不为空时显示在 from 「」之后
```

```javascript
  "no_stream": boolean,
    // 本曲是否能够在直播模式中游玩
  
  "jacket_localized": {
    "ja": boolean ...
  },// 自定义本曲封面，可分语言设定。封面文件名为base_ja.jpg，base_ja_256.jpg（即在base后加“_语言代码”）
}
```

#### **难度信息**

难度谱面信息框架如下：

```javascript
  "difficulties": [
    {
      // difficulty PST
    } ...
  ]
```

各难度代码结构如下：

```javascript
    {
      "ratingClass": int (0, 1, 2, 3),
        // 本段代码所定义难度。0 -- PST, 1 -- PRS, 2 -- FTR, 3 -- BYD 必需字段 3.0修改
      
      "chartDesigner": string,
        // 本难度谱师名 必需字段
      
      "jacketDesigner": string, 
        // 本难度封面绘师 必需字段
      
      "rating": int,
        // 本难度等级。3.0更新前1-9对应本身，10对应9+，11对应10；3.0更新后均为本身。0均对应?  必需字段 3.0修改
      
      "ratingPlus": boolean,
        // 本难度等级是否有“+” 3.0新增
      
      "plusFingers": boolean,
        // 本难度是否有多指操作，实际并无作用
      
      "jacket_night": string (ASCII),
        // 本难度夜晚时显示的封面文件名 只能使用ASCII字符
      
      "jacketOverride": boolean,
        // 本难度是否有根据难度替换的封面。封面文件名为0.jpg，0_256.jpg（即为"ratingClass"）
      
      "hidden_until_unlocked": boolean,
        // 本难度解锁前是否歌曲界面中隐藏 3.0新增
      
      "bg": string (ASCII),
        // 自定义本难度背景名，背景jpg储存在\assets\img\bg目录中 只能使用ASCII字符
      
      "world_unlock": boolean
        // 本难度是否需要世界模式解锁，尚无法使用
    }
```

