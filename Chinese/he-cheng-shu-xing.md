# 合成属性

## .合成属性窗口（Properties/属性）

合成属性窗口位于编辑器整体窗口的右侧。

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

窗口不具备滚动条，但是可以通过在窗口区域混动鼠标中键滚轮来进行上下翻页（请自备带滚轮的鼠标）

## 2.片段属性（Part/片段）

### 2.1 增益（Gain）

<figure><img src=".gitbook/assets/image-1 (1).png" alt=""><figcaption></figcaption></figure>

增益的值域时-12db到12db，用于整体调整当前片段的音量。主要作用是用来平衡不同声库之间的基础音量差距。

### 2.2 最小切分片段(MinSegmentSpacing)

最小切片分段用于控制渲染队列。当两个音符之间的间距小于等于这个值时，两个音符将被视作连续的发音而划归到同一个渲染任务中渲染。

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

渲染任务分片越多，渲染速度越快。因此适当的设置此值有助于更好的使用体验。默认值是0，即音符只有前后连续时才算作同一个渲染任务。

### 2.2 滑音过度时长(PitchTransitionTiming)

在同一个渲染任务中，两个连续的音符之间会自动产生过度滑音。这个过度滑音的持续时间由本参数控制。参数单位是秒，默认值是0.12（即120毫秒）。

<figure><img src=".gitbook/assets/image-1 (2).png" alt=""><figcaption></figcaption></figure>

本属性值的中位点是前一个音符的结束点， 即滑音始终占用前一个音符末尾的 (PitchTransitionTiming/2)秒的长度用来滑音。

### 2.3 音素器选择（Phonnemizer)

具体功能见“安装与卸载与基本输入”一节的说明。

### 2.4 音高精度(PitchResolution)

共三个选项，Ultra、Normal、Electionic。控制音高曲线的采样点精度。

Ultra控制精度为1ms一个控制点，精度最高，渲染最慢。且需要引擎支持超高速采样（Tempo>512)

Normal精度为5ms一个控制点，为Utau标准精度

Electronic为高速采样控制点，渲染最快，但精度最低。但是自带音高对齐，相当于挂了AutoTune插件。

### 2.5 音符级压缩(Flags:Peakcompressor)

Utau标准引擎Flags: p

针对音符的压缩器，默认值是0.86。

### 2.6 拉伸方式(Flags:e)

Utau标准引擎Flags: e以及Mocaloid引擎标签Me

选择音符的拉伸方式，默认为自动判别。

## 3.片段属性（Part/片段） - 音效器AFX

此段为插件内置的音频效果器，用于修正或者直接作为效果器使用。

### 3.1 压缩器参数（AFX:Compressor)

thresholdDb:限幅

ratio:压缩比例

BoosterDb:压缩后音量Gain调整

AttrackTime:压缩启动时间

ReleaseTime:压缩释放时间

### 3.1 带通EQ参数（AFX:EQ)

中心频率:  |   60Hz   |    250Hz    |     1kHz    |    4kHz   |     16kHz     |

Q:               |      1.7      |        1.7       |      1.6       |     1.7       |       1.7          |

### 3.3 混响器参数（AFX:Reverb)

Mix:干湿比

Delay:延迟(ms/100)

DecayFactor:空间反射倍率

## 4.自动化参数属性（Automation/参数)

此处的自动化参数滑动杆作用与“自动化参数”一节一致，用于整体平移自动化参数一节中参数窗口的值。因此不再过多介绍。

## 5.音符属性(Note/音符）

音符属性是针对当前选中的一个或多个音符的音符设置。

### 5.1 抢先发音（EarlyStart）

<figure><img src=".gitbook/assets/图片 (19).png" alt=""><figcaption></figcaption></figure>

用于在不改变实际音符位置的情况下调整相邻音符的发音起点，当earlyStart>0时，音符起始点向前移动（前序音符相应缩短），当earlyStart<0时，音符起始点向后移动，前序音符相应拉长。

### 5.2 辅音速度（Velocity）

此参数用于修改选中音符的辅音速度

### 5.3 采样前缀（PrefixPair）

用于选择采样前缀锁定采样发音，默认AutoSelect为根据Premap.map文件定义自动匹配使用的采样。

### 5.4 升降调（Flags:Toneshift）

通过调节该值可以直接对发音的音高进行升降。

### 5.5 辅音气声(Flags:breath)

标准Utau的Flag参数b。是对于清辅音振幅的增益值。

### 5.6 开口度（Flags:Opening)（Moresampler特有）

设置发音的开口度口型。

### 5.7 XSP控制参数(XTrack: \*)

见自动化参数一节

<figure><img src="../.gitbook/assets/image%20(27).png" alt=""><figcaption></figcaption></figure>
