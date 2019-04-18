# 用树莓派搭建FM广播，播放音乐和实时语音

> 树莓派开启FM广播台，广播指定的音乐或实时语音<br>
>
> 本教程仅供科研与学习交流之用，广播功率很小。请务必遵守国家相关电信管理法规。<br>
>
>  基本原理：从奥斯特、法拉第，到麦克斯韦，从电容、电感到电磁波天线。<br>
>
> [本文配套B站视频：子豪兄的树莓派零基础教程](https://space.bilibili.com/1900783/#/)<br>

![树莓派FM广播站](https://upload-images.jianshu.io/upload_images/13714448-353a04e7344f703b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

【子豪兄的树莓派零基础教程】第5讲：用树莓派搭建FM广播电台，播放音乐和实时语音<br>

作者：张子豪（同济大学在读研究生）<br>

博客文档、源代码、更新、勘误，请看[本教程Github代码仓库](https://github.com/TommyZihao/ZihaoTutorialOfRaspberryPi)<br>

知乎、简书专栏：**人工智能小技巧**<br>

# 粉丝答疑交流QQ群：`953712961`<br>

# 微信赞赏二维码

![微信扫码支持子豪兄制作树莓派教程](https://upload-images.jianshu.io/upload_images/13714448-4be7dc29e22207b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)



# 目录

-   [材料准备](#材料准备)
-   [安装配置](#安装配置)
-   [广播内置歌曲：吉他音乐](#广播内置歌曲吉他音乐)
-   [广播歌曲：星球大战](#广播歌曲星球大战)
-   [广播实时语音](#广播实时语音)
-   [潜在应用领域](#潜在应用领域)
-   [声明](#声明)
-   [调频广播和天线基本原理](#调频广播和天线基本原理)
    -   [高中物理课本相关内容](#高中物理课本相关内容)
    -   [电波发射与信号采样](#电波发射与信号采样)
    -   [调频与调幅搭载信息](#调频与调幅搭载信息)
    -   [PWM：脉冲宽度调制](#pwm脉冲宽度调制)
    -   [树莓派的硬件基础：CPU、GPIO](#树莓派的硬件基础cpugpio)
    -   [DMA直接内存访问与扩频时钟](#dma直接内存访问与扩频时钟)
    -   [调频得到传输信号](#调频得到传输信号)
    -   [树莓派天线长度](#树莓派天线长度)
    -   [传播距离估计](#传播距离估计)
-   [扩展阅读与参考文献](#扩展阅读与参考文献)



# 材料准备

- 树莓派3B或树莓派3B+<br>

- SD卡已烧录好系统并完成一系列配置（换源等），具体操作可按照[第3讲：一劳永逸配置树莓派【子豪兄的零基础树莓派教程】](<https://www.bilibili.com/video/av48281861>)步骤一步步进行<br>

- 一台收音机，或安装有收音机app的手机<br>

- （可选）麦克风。用于广播实时语音<br>

- （可选）USB声卡。用于广播实时语音<br>

  ![USB声卡](https://upload-images.jianshu.io/upload_images/13714448-93e61fbf524a72c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  > 声卡是干啥的？
  >
  > 声卡是将话筒接受到的外界声音信号（连续的模拟信号）转换为离散数字信号（数模转换）并传输给计算机（树莓派）进行处理的数字电路。USB声卡就是通过USB口提供声音功能（耳机、麦克风）的装置。

# 安装配置


在树莓派的命令行界面依次运行以下八条命令

```shell
mkdir fm

cd fm

sudo git clone https://github.com/markondej/fm_transmitter

sudo apt-get install mpg123

sudo apt-get install gcc g++ make

cd fm_transmitter

sudo make

sudo apt-get install sox
```

> 注意，后文的所有命令都需要在`fm/fm_transmitter`目录下执行。可以通过`cd fm/fm_transmitter`命令切换到这个目录下。

# 广播内置歌曲：吉他音乐

```shell
sox acoustic_guitar_duet.wav -r 22050 -c 1 -b 16 -t wav - | sudo ./fm_transmitter -f 100.6 -
```
![广播吉他音乐](https://upload-images.jianshu.io/upload_images/13714448-0514b0cc0162d927.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>也可以把这条命令中的100.6改成其它数字，即可在新频道上广播。不要和已有电台频率冲突。
>
>也可以将你自己的wav格式的声音文件放到/fm/fm_transmitter文件夹中，替换命令中的star_wars.wav文件。
>
>WAV是最接近无损的音乐格式，所以文件也比较大。
>
>在树莓派GPIO的BCM4号引脚上接一条跳线，可以提升广播效果。
>
>本教程仅供科研与学习交流之用，广播覆盖范围不超过十米。如想搭建大功率电台请遵守国家法律法规按正规流程申请备案。（请看文末[声明](#声明)）

![接线图](https://upload-images.jianshu.io/upload_images/13714448-4f57e56124e309e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



![树莓派GPIO上的BCM4号引脚](https://upload-images.jianshu.io/upload_images/13714448-7496dbe9e2e994f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 广播歌曲：星球大战

```shell
sudo git reset --hard 71e7e23a0e

sox star_wars.wav -r 22050 -c 1 -b 16 -t wav - | sudo ./fm_transmitter -f 100.6 -
```

![广播星球大战音乐](https://upload-images.jianshu.io/upload_images/13714448-e2d101ad652b0786.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

按`ctrl`+`c`结束广播。

> `git reset`命令是使所在目录回退到之前的指定版本，如果你想切换回最新版本，可以运行`sudo git reset --hard 6111460`命令。

# 广播实时语音

![语音实时广播](https://upload-images.jianshu.io/upload_images/13714448-c69cd506673c5bfb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在树莓派的USB口插上USB声卡，在USB声卡的麦克风孔里插入麦克风，运行以下命令，在即可在调频100.6MHz频道广播实时语音，你也可以把这条命令中的100.6改成其它数字，那样就会在新频道上广播：

```shell
arecord -D plughw:1,0 -c1 -d 0 -r 22050 -f S16_LE | sudo ./fm_transmitter -f 100.6 -
```

按`ctrl`+`c`结束广播。



# 潜在应用领域

用移动电源给树莓派供电，设置开机免密码自动登录和自动运行广播脚本，将整个系统装在书包里，即可实现走到哪里，广播开到哪里（旅游景点、重要会场讲话、窃听器、位置信标）。与无线供电或太阳能相结合，可以实现半永久性的窃听广播站。

应用领域：警用军用情报、边防与国家安全、智能安保安防、环境灾害、地质灾害预警

例如，大佬做讲座的报告厅人满为患，就可以做一个fm广播站，让堵在门外的人也能听到实时语音。

例如，如果有窃贼或非法入侵者触发了信号（如红外探头、微动开关等），就立刻开启fm广播电台。

例如，树莓派每次开机的时候都在指定频段广播自己的ip地址。



# 声明

> 本教程仅供科研与学习交流之用，广播覆盖范围不超过十米。如想搭建大功率电台请遵守国家法律法规按正规流程申请备案。<br>
>
> [中华人民共和国无线电管理条例](<http://www.srrc.org.cn//2017/tiaoli/tiaoli.aspx>)<br>
>
> 摘录：<br>
>
> 第五条 国家鼓励、支持对无线电频谱资源的科学技术研究和先进技术的推广应用，提高无线电频谱资源的利用效率。<br>
>
> 第十四条 使用无线电频率应当取得许可，但下列频率除外：<br>
>
> （一）业余无线电台、公众对讲机、制式无线电台使用的频率；<br>



# 调频广播和天线基本原理

参考资料：[知乎：树莓派 FM 发射机小电台原理解析](<https://zhuanlan.zhihu.com/p/58126434>)<br>

## 高中物理课本相关内容

![幻灯片3.JPG](https://upload-images.jianshu.io/upload_images/13714448-e3f346e2df5e3136.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![幻灯片4.JPG](https://upload-images.jianshu.io/upload_images/13714448-aa4ffe6a81f08ef3.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![幻灯片5.JPG](https://upload-images.jianshu.io/upload_images/13714448-e2497f296f9d0b1b.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![幻灯片6.JPG](https://upload-images.jianshu.io/upload_images/13714448-d668793b519cb460.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![幻灯片7.JPG](https://upload-images.jianshu.io/upload_images/13714448-2f5a80fe799c32c2.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![幻灯片8.JPG](https://upload-images.jianshu.io/upload_images/13714448-c58838119b3376cb.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![幻灯片9.JPG](https://upload-images.jianshu.io/upload_images/13714448-f1b494f4ad54f21f.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![幻灯片10.JPG](https://upload-images.jianshu.io/upload_images/13714448-9bf6196de14c26dd.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![幻灯片11.JPG](https://upload-images.jianshu.io/upload_images/13714448-12b432d586aed38c.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 电波发射与信号采样

![调制电磁波信息](https://upload-images.jianshu.io/upload_images/13714448-099650080aacc582.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

信号采样
![信号采样](https://upload-images.jianshu.io/upload_images/13714448-6e6e5bb22a4fcb60.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 调频与调幅搭载信息

![调频与调幅](https://upload-images.jianshu.io/upload_images/13714448-54cd18701adfc106.gif?imageMogr2/auto-orient/strip)

## PWM：脉冲宽度调制

PWM脉冲宽度调制(Pulse Width Modulation) 是使用离散的数字信号生成连续的模拟信号的方法。主要由 2 个参数来定义：**占空比**和**频率**。如果以保持一定的速率开关数字信号并且保持一定的占空比，那么输出看起来就像恒定电压模拟信号。

![PWM](https://upload-images.jianshu.io/upload_images/13714448-02bd2faed695bb68.gif?imageMogr2/auto-orient/strip)

## 树莓派的硬件基础：CPU、GPIO



![树莓派3B的CPU芯片](https://upload-images.jianshu.io/upload_images/13714448-abebf88882288201.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![GPIO四号引脚](https://upload-images.jianshu.io/upload_images/13714448-a063582f5f346c5b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



## DMA直接内存访问与扩频时钟

DMA: 直接内存访问(Direct Memory Access)。不用跟CPU打招呼就可以直接访问内存。

![DMA：直接访问内存](https://upload-images.jianshu.io/upload_images/13714448-647a379fa6f404a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

绝大多数的的微处理器都有扩频时钟(Spread-spectrum clock)，目的是为了降低电磁干扰(EMI)，在树莓派 BCM28XX 系列芯片上，扩频时钟的范围为 1MHz 到 250MHz，这正好用作 FM 的载波信号。

为了减少CPU占用，作者对程序进行了改进，使用树莓派 DMA 产生基础时钟。

![时钟信号](https://upload-images.jianshu.io/upload_images/13714448-d1c9ffd112bde2f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![扩频时钟](https://upload-images.jianshu.io/upload_images/13714448-eb35e6c1c87e4ac5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 调频得到传输信号

基带信号 ![x_{m}(t)](https://www.zhihu.com/equation?tex=x_%7Bm%7D%28t%29) ，载波频率 ![ f_{c}](https://www.zhihu.com/equation?tex=+f_%7Bc%7D) ，正弦载波为 ![x_{c}(t)=A_{c} \cos \left(2 \pi f_{c} t\right)](https://www.zhihu.com/equation?tex=x_%7Bc%7D%28t%29%3DA_%7Bc%7D+%5Ccos+%5Cleft%282+%5Cpi+f_%7Bc%7D+t%5Cright%29) 将基带数据信号与载波结合起来得到了传输信号

![调频公式](https://upload-images.jianshu.io/upload_images/13714448-903c3340f0d930d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



其中 ![f(\tau)](https://www.zhihu.com/equation?tex=f%28%5Ctau%29) 为传输信号的瞬时频率， ![f_{\Delta}](https://www.zhihu.com/equation?tex=f_%7B%5CDelta%7D) 为频偏表示相对载波频率 ![f_{c}](https://www.zhihu.com/equation?tex=f_%7Bc%7D) 的最大频率偏移。

调频输出的是模拟信号，利用时钟产生 PWM 调整占空比和频率，就可以利用数字信号生成模拟信号。

## 树莓派天线长度

- **波长**： ![\lambda=c/f](https://www.zhihu.com/equation?tex=%5Clambda%3Dc%2Ff)
- **偶极子天线**：制作偶极子天线时，会通过工作波长来确定天线的长度。最常见的偶极子天线是半波天线，它的总长度近似为工作波长的一半，即 ![ L=\lambda / 2](https://www.zhihu.com/equation?tex=+L%3D%5Clambda+%2F+2)

![天线](https://upload-images.jianshu.io/upload_images/13714448-83cf7f07d04ed1d7.gif?imageMogr2/auto-orient/strip)

如果需要发射100MHz的FM信号,根据上面的公式来计算，就需要1.5m长的天线。

```python
>>> 3*10**8 / (2 * 100 * 10**6)
1.5
```

所以理论上如果给树莓派 GPIO(PIN4) 加上了一根 **1.5m** 的天线，那么就可以输出最大功率的 FM 信号。

## 传播距离估计

首先需要计算有效全向辐射功率(EIRP)

![EIRP = P - Loss +G](https://www.zhihu.com/equation?tex=EIRP+%3D+P+-+Loss+%2BG)

其中 *P* 为发射机的输出功率(*dBm*)，*Loss* 为发射机输出端与天线馈源之间的馈线损耗(*dB*)，*G* 为天线的发送增益(*dBi*)。求出 EIRP 后可以进而获得自由空间路径损失（Free Space Path Loss，FSPL）。

但是使用这个公式估算，意义不是太大。实际测量，如果使用一根 10cm 的杜邦线作为天线，一个楼梯拐角信号就已经非常弱了。

 

# 扩展阅读与参考文献

> [让树莓派说出自己的ip地址](https://www.cnblogs.com/ma6174/archive/2013/09/29/3345278.html)
>
> [Bilibili视频：【熟肉】教你用树莓派制作可以进行语音直播的FM调频无线电台](https://www.bilibili.com/video/av23299793/?spm_id_from=333.788.videocard.1)
>
> [知乎：树莓派 FM 发射机小电台原理解析](<https://zhuanlan.zhihu.com/p/58126434>)<br>
>
> 国外参考文献：
>
> - [1] Eben Upton and Gareth Halfacree. Raspberry Pi user guide. John Wiley & Sons, 2014.
> - [2] Oliver Mattos and Oskar Weigl. Turning the Raspberry Pi Into an FM Transmitter. [http://www.icrobotics.co.uk/wiki/index.php/Turning](https://link.zhihu.com/?target=http%3A//www.icrobotics.co.uk/wiki/index.php/Turning) the Raspberry Pi Into an FM Transmitter, 2015.
> - [3] Christophe Jacquet. FM-RDS transmitter using the Raspberry Pi’s PWM . [https://github.com/ChristopheJacquet/PiFmRds](https://link.zhihu.com/?target=https%3A//github.com/ChristopheJacquet/PiFmRds), 2014.
> - [4] Richardson. Turning the Raspberry Pi Into an FM Transmitter. [http://www.icrobotics.co.uk/wiki/index.php/Turning_the_Raspberry_Pi_Into_an_FM_Transmitter](https://link.zhihu.com/?target=http%3A//www.icrobotics.co.uk/wiki/index.php/Turning_the_Raspberry_Pi_Into_an_FM_Transmitter), 2015.

![子豪兄的树莓派系列教程](https://upload-images.jianshu.io/upload_images/13714448-bc64c10051174fde.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![微信扫码支持子豪兄制作树莓派教程](https://upload-images.jianshu.io/upload_images/13714448-4be7dc29e22207b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

![树莓派接线](https://upload-images.jianshu.io/upload_images/13714448-d706c8c62aa45125.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/842/format/webp)

![欢迎加入树莓派全球开源社区](https://upload-images.jianshu.io/upload_images/13714448-9413183a2d79c2a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

