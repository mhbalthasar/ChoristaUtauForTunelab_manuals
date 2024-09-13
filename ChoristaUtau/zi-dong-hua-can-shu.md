# 自动化参数

## 1.线性自动化参数和非线性自动化参数

**线性自动化参数**是至按照时间精确控制时间点值的参数，ChoristaUtau插件中主要的线性自动化参数有：音量（Volume），音高(Pitch,直接绘制），颤音包络(VibratoEnvlope)和线性混合(XSP)

**非线性自动化参数**对应Utau引擎中的Flags参数标记，该类型参数针对的是某个发音单元，考虑到拆音后数值的线性变化，因此以自动化参数的形式体现其变化。

**1.1 非线性自动化参数的取值**

<figure><img src=".gitbook/assets/图片 (13).png" alt=""><figcaption></figcaption></figure>

非线性自动化参数的取值主要取自音素头部分割线（途中灰色线为分割线）位置的值。值的作用域是整个音素。如红色线位置的值作用域就是音素-e

考虑到要求精确定位，参数设置复杂性较高，读取时会有偏移容差（图中彩色方框范围),容差通常最大不超过30ms或者音素的一半长度。实际效果形成额隐性条带效果如图中橙色矩形所示（类似Vocaloid中OPE样式的条带参数）

**1.2 非线性自动化参数中的特例1：RLE参数**

<figure><img src=".gitbook/assets/图片 (15).png" alt=""><figcaption></figcaption></figure>

RLE参数用于设置音素渐出时的起始音量，作用位置是音素实际发音的尾部，因此参数设置值的读取点位被调整到了尾部的分割线（如图所示）

**1.3 非线性自动化参数中的特例2：PRE/OVL/FXL/LBD/RBD参数**

此类参数是直接操作元音设定的危险参数（虽然已经尽可能去掉了非法值），因此为了避免错误触发，此类参数与其他非线性自动化参数相比，去掉了偏移容差。也就是说值必须设置在分割线所在位置才有效。

## 2.UTAU通用引擎参数

### 2.1 性别（g/Flags:gender）

通过调整第一和第二共振峰的距离改变声音的性别特征。影响声音的结构。数值越高，男性的感觉越强；越低，则变成女性甚至幼儿的声音。

数值越大越偏男性，越小越偏女性。

实际应用中也会被用来调整唱腔，当发生真假声变换时通常需要微调性别参数。

### 2.2 线性混合（XSP/XTrack Synthesis Percent）

UTAU引擎的绝大多数参数都是非线性的，这对于较长的发音控制会产生困难。同时多采样的声库，生线的自然融合也有需求。此时可以通过线性混合参数实现线性控制。

线性混合的原理是对两条已经合成完的生线进行数值上的动态融合。

被融合的第一条声线是合成的当前生线，默认融合占比是100%，随着XSP逼近1.0而线性减低至0%

<figure><img src=".gitbook/assets/图片 (16).png" alt=""><figcaption></figcaption></figure>

被融合的第二条声线是基于第一条声线变化而来，默认可以设置新采样（XTrack:PrefixPair)和性别差值(XTrack:gender Corrected)。其他Flags值是个性化引擎提供的，其中Moresampler提供了Opening，Tense和Breathness参数。

除了采样参数是直接替换外，其余声线参数的值是通过偏移计算获得的。以性别参数为例：第二条声线的参数g2=第一条声线的参数g+差值genderCorrected

### 2.3 原音设定调整（**PRE/OVL/FXL/LBD/RBD**）

一般情况建议调整此值，UTAU大手子可以尝试。

具体公式：最终值=OTO原始值+线性参数值

例如左边界(Offset)   Offset=OtoOffset + LBD

调整时，程序内部做了换算，单项设定调整不会影像有关值的位置。如：调整LBD不会影像PRE的实际位置。如果希望联动调整，请进行数值同步（即同时调整LBD和PRE、OVL、FXL的值）

## 3.Moresampler个性化引擎参数

<figure><img src=".gitbook/assets/图片 (17).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/图片 (18).png" alt=""><figcaption></figcaption></figure>

### 3.1 调整共振(Mr/Flags:MReson)

### 3.2干涩度(Md/Flags:Mdryess)

合成过程中气息（主要是呼气音）的强度，数值越强，VOCALOID模拟出声音的”声带“本音占比越小。

数值越高，气声越强，当调节到最大值时，会形成说悄悄话的耳语效果。

### 3.3 张力（Mt/Flags:Mtense）

设置合成中声线的放松程度。

### 3.4嘶吼音(MG/Flags:Mgrowl)

通过模拟情绪激动时咆哮的声音不稳定性来拟合情绪。通过混入特定的噪音，使歌手的声音产生嘶吼的效果。

通常只用作节奏特别强烈的“燃曲”，使用时输出波形的抖动程度会显著增加。

### 3.5粗糙度(MC/Flags:MCrude)

### 3.6呼吸强度(Mb/Flags:Mbreathness)

合成过程中气息（主要是吸气音）的强度，数值越强，VOCALOID模拟出声音的”声带“本音占比越小。

数值越高，气声越强，当调节到最大值时，会形成说悄悄话的耳语效果。

### 3.7失真（MD/Flags:MDistort)

### 3.8强化共振(ME/Flags:MEnhance)

###
