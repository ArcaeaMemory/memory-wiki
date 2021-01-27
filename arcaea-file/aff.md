# 谱面格式

* **警告，lowiro明确讲过禁止传播官方以外的版本，这里只是谱面格式的介绍帖，自制谱一切后果自负！**

  [由259WA777撰写的谱面解析](https://tieba.baidu.com/p/5015977438)

以下是在上述解析的基础上编写的。

## 总论

谱面的后缀名为aff，所有官方谱面在apk安装包中并没有加密，可以直接阅读。

谱面所在位置为\assets\songs\\(歌曲文件名\)里，其中0,1,2,3分别对应PST,PRS,FTR及BYD。~~其他的是什么东西自己打开便知道了~~

理论上更改aff文件以及对应音源后重新正确封包即可游玩。

## 解析

### 文件头

所有谱面开始都为以下两行代码

```text
AudioOffset:x
-
```

这行代码表示音乐整体往前\(-\)/往后\(+\)移动x毫秒

推荐x=0，这样你物件对应的毫秒数即为歌曲对应的音的毫秒数。

**但是如果x≠0，你的物件对应毫秒数应为\(音对应的毫秒数+x\)**

_鉴于有些音源以开头为基准第一个采音不在整拍上，可能有时候你真的需要x≠0。_~~_懒得算了_~~

有的谱面会在AudioOffset行下方加入一行TimingPointDensityFactor：

```text
TimingPointDensityFactor:x
```

这行代码表示音弧和长条的物量密度调整为正常值的x倍

x=1时效果与省略此行相同

~~如果x的值特别大的话...~~

在该文件里并没有曲名，谱师之类的歌曲信息，请移步[歌曲信息\(songlist\)格式](https://wiki.arcaea.cn/index.php/%E6%AD%8C%E6%9B%B2%E4%BF%A1%E6%81%AF%28songlist%29%E6%A0%BC%E5%BC%8F)

如果想更改关于解歌条件的部分，请移步[解锁条件\(unlocks\)格式](https://wiki.arcaea.cn/index.php/%E8%A7%A3%E9%94%81%E6%9D%A1%E4%BB%B6%28unlocks%29%E6%A0%BC%E5%BC%8F)

如果想更改曲包相关内容请移步[曲包信息\(packlist\)格式](https://wiki.arcaea.cn/index.php/%E6%9B%B2%E5%8C%85%E4%BF%A1%E6%81%AF%28packlist%29%E6%A0%BC%E5%BC%8F)

### Timing

Timing代码如下

```text
timing(Offset,BPM,Beats);
```

* Offset\(ms\):Timing起始位置，数字为整数
* BPM\(拍/分钟\):节奏速度，数字为不可省略小数点后两位的一个数
* Beats\(四分音个数\(拍\)\):表示每多少个四分音符\(拍\)为一小节（出现一条小节线），数字为不可省略小数点后两位的一个数，比如4.00就是4/4拍，四拍一小节
* **需要注意的是一定有一个Offset=0的Timing！**

### 地面Note & 地面Hold

地面Note & 地面Hold代码如下

```text
(t,lane);
hold(t1,t2,lane);
```

* t\(ms\):地面Note所在时间，数字为整数
* t1,t2\(ms\):地面Hold物件开始/结束的时间，数字为整数，**t1＜t2**
* lane\(1～4\):物件所在轨道，从左到右分别为1,2,3,4

### 虹弧Arc & 天空Note

虹弧Arc & 天空Note代码如下

```text
arc(t1,t2,x1,x2,slideeasing,y1,y2,color,FX,skylineBoolean);
```

* t1,t2\(ms\):虹弧Arc物件开始/结束的时间，数字为整数，**t1可以等于t2**，当t1=t2时，虹弧与判定线平行，物量为0。
* x1,x2\(-0.50～1.50\):代表Arc物件开始/结束时的横坐标，**数字为不可省略小数点后两位的一个数**
* slideasing\(b,s,si,so\):虹弧滑动方式。b=Both=Sine in & out，s=straight，si=Sine in，so=Sine out。**当t1=t2时该参数无意义，都是直的**
  * si与so可以两个在一起自由组合\(如siso,sisi等\)，siso代表x方向上滑动方式为si、y方向上滑动方式为so
* y1,y2\(0.00～1.00\):代表Arc物件开始/结束时的纵坐标，**数字为不可省略小数点后两位的一个数**
* color:虹弧颜色，0蓝，1红，2绿，**在skylineBoolean=true时该参数无意义**
* FX\(none,full,incremental\):目前尚未发掘出该参数的用途，已知本参数可以填none，full，incremental，可实际上填写时并没有区别 lowiro模仿SDVX的证明\(
* skylineBoolean\(false,true\):判定这一段虹弧是不是天空Note的判定线。false为普通虹弧，true为天空Note的判定线。但是只要有Arctap本参数就无意义，都为黑线
  * 当skylineBoolean=true，并且该判定线上有天空Note时，代码如下

```text
arc(t1,t2,x1,x2,slidemethod,y1,y2,color,FX,true)[arctap(tn1),arctap(tn2),……,arctap(tnm)];
```

* tn1,tn2,……,tnm\(ms\):m个天空物件在这条判定线上的时间点，数字为整数，且不能超出t1和t2的区间

### 综合

代码排列顺序**除了第一个offset=0的Timing外**不受限制。

**还是一句老话，编完请自己high你不要大规模传播!!!**

### 1.6.1新特性

* arc语句中，x1 x2 y1 y2参数可以超出限制
* 新增camera语句

  * 位置在第一个Timing语句下方，**不混杂在真正note语句里**，按时间顺序排列，用一个空行与真正note语句分开

  ```text
  camera(t,transverse,bottomzoom,linezoom,steadyangle,topzoom,angle,easing,lastingtime);
  ```

  * t\(ms\):camera开始时间
  * transverse:轨道底部左右横向移动,正←负→.
  * bottomzoom:轨道底部上下移动,正↓负↑
  * linezoom:判定线前后移动,正远离负靠近
  * steadyangle\(°\):原地的摄像头视角转向,正逆时针负顺时针
  * topzoom:轨道顶部的上下移动,正↓负↑
  * angle\(°\):底盘依照屏幕中心旋转,正逆时针负顺时针
  * easing\(qi,qo,l,reset,s\):cubicin,cubicout,line,reset,sinein&out
  * lastingtime\(ms\):本语句持续时间
  * 本功能在1.7.0在代码中被标记关闭，1.8.0中相关代码被彻底删除，但在之后的愚人节版本中被恢复

### 2.0.2新特性

* camera回来了,添加s转换属性
* 添加绿arc，color值为2，并且只有愚人节版本才能读取绿arc

### 2.6.1新特性

* camera和绿arc回来了
* 新增scenecontrol语句

  ```text
  scenecontrol(t,type);
  ```

  * t\(ms\):场景开始时间
  * type\(trackhide,trackshow\):是否展示轨道

### 3.0.0新特性

* 新增timinggroup语句块

  ```text
  timinggroup(){
   //xxx
  };
  ```

  * 每一个timinggroup语句块中的语句使用其内部单独的timing语句，因此可以实现同时刻不同note流速。
  * timinggroup语句块中的timing语句不会产生小节线
  * 一张谱面理论可以存在无限多个timinggroup语句块。

* scenecontrol语句修改参数

  ```text
  scenecontrol(t,type,x,y);
  ```

  * t\(ms\): 场景开始时间
  * type:
  * trackdisplay: 展示轨道
  * redline: Arcahv解锁表演时的背景红线效果
  * arcahvdistort: Arcahv解锁表演时的背景变形效果
  * arcahvdebris: Arcahv解锁表演时的背景碎片效果
  * x\(float\): 未知参数
  * y\(int\): 未知参数

## 物量计算

有的时候我们并不能玩到自制谱面，这个时候我们可以通过以下方式计算本谱物量：

* 统计所有地面note和arctap以及flick数量，每统计一个+1
* Hold物件逐个计算，每个hold被起始位置所在BPM的osu 1/4拍\(也就是SDVX的1/16小节\)\[说明：即判断间隔毫秒数是60000/bpm/2\]分成一个一个判定块，**每个判定块开始处物量+1**。
  * 特殊的，每个Hold最后一个判定块不加物量
  * BPM＞=255时，判定块间隔变为所在BPM的osu 1/2拍\(也就是SDVX的1/8小节\)
  * BPM=0时，**本物件不存在**，更无从谈及物量
  * BPM＜0时，按BPM的绝对值进行计算
  * 当Hold长度短于本来的判定块长度时，整个物件对半分为两个判定块\(**无论如何最后一个判定块不计入物量**\)
  * 当Hold跨越timing时，按Hold起始点的BPM进行计算
* Arc物件基本与Hold相同，**注意每个arc语句单算**
  * 持续时长为0的arc物量为0
  * skylineBoolean为true时物量为0
  * Arc可以连接形成arc组，此时头蛇按照Hold方式计算，其它蛇物量+1
    * 连接条件：与arc颜色无关，要求前一个arc结尾和后一个arc开头x坐标差小于0.1，y坐标相等，时间差小于10

_需要指出，Hold和Arc可能会出现误差，原因在于末尾处可能刚好超过计数点零点几毫秒，不过即使如此正常情况下误差总计也不会太大。_

