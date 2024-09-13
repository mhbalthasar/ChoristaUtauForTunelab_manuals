# 音符录入

## 1.歌词的录入

此部分内容请查阅TuneLab编辑器说明文档。

## 2.发音符号的录入

当歌词的发音不符合发音要求时，可以通过直接录入发音符号的方式实现音符发音。

### 2.1 通过“.”符号录入

在录入歌词时，可以通过添加保留记号“.”来实现直接录入发音符号。Utau的直接发音符号是针对当前音符整音的，因此主要用于作为整音拆音

<figure><img src=".gitbook/assets/图片 (10).png" alt=""><figcaption></figcaption></figure>

考虑到连续拆音的情况，当使用单个“."号作为前导时，系统会尽可能猜测当前发音的元音和辅音用于支持拆音：

<figure><img src=".gitbook/assets/图片 (11).png" alt=""><figcaption></figcaption></figure>

当使用连续两个“.”作为前导时，则完全将发音视作整体，不进行额外考虑

### 2.2 通过音符歌词录入（仅OU兼容插件支持）

对于音节化的歌词和OU兼容的CVVC插件，系统额外支持了Openutau类似的歌词Hit功能，通过中括号包裹的发音符号会作为匹配音节进行音素录入。

<figure><img src=".gitbook/assets/图片 (12).png" alt=""><figcaption></figcaption></figure>

