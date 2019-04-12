# 用树莓派搭建FM广播，播放音乐和实时语音

> 树莓派开启FM广播台，广播指定的音乐或实时语音<br>
>
> 本教程仅供科研与学习交流之用，广播功率很小。请务必遵守国家相关电信管理法规。<br>
>
> [本文配套B站视频：子豪兄的树莓派零基础教程](https://space.bilibili.com/1900783/#/)<br>

第5讲：用树莓派搭建FM广播电台，播放音乐和实时语音【子豪兄的树莓派零基础教程】<br>

作者：张子豪（同济大学在读研究生）<br>

博客文档、源代码、更新、勘误，请看[本教程Github代码仓库](https://github.com/TommyZihao/ZihaoTutorialOfRaspberryPi)<br>

知乎、简书专栏：**人工智能小技巧**<br>

# B站粉丝QQ群号：`953712961`

![广播台](https://upload-images.jianshu.io/upload_images/13714448-9df47671e18e9812.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



-   [材料准备](#材料准备)
-   [安装配置](#安装配置)
-   [广播内置歌曲：星球大战](#广播内置歌曲星球大战)
-   [广播实时语音](#广播实时语音)
-   [扩展应用](#扩展应用)
-   [声明](#声明)
-   [扩展阅读与参考文献](#扩展阅读与参考文献)

# 材料准备

- 树莓派3B或树莓派3B+

- SD卡已烧录好系统并完成一系列配置（换源等），可参考[第3讲：一劳永逸配置树莓派【子豪兄的零基础树莓派教程】](<https://www.bilibili.com/video/av48281861>)<br>

- 一台收音机，或安装有收音机app的手机

- （可选）USB声卡。用于广播实时语音。

  ![USB声卡](https://upload-images.jianshu.io/upload_images/13714448-93e61fbf524a72c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  > 声卡是干啥的？
  >
  > 声卡的作用是将话筒接受到的声音信号（模拟信号）转换为数字信号（数模转换）并传输给计算机（树莓派）的装置。USB声卡就是通过USB口提供声音功能（耳机、麦克风）的装置。

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

# 广播内置歌曲：吉他音乐

```shell
sox acoustic_guitar_duet.wav -r 22050 -c 1 -b 16 -t wav - | sudo ./fm_transmitter -f 100.6 -
```

>也可以把这条命令中的100.6改成其它数字，即可在新频道上广播。不要和已有电台频率冲突。
>
>也可以将你自己的wav格式的声音文件放到/fm/fm_transmitter文件夹中，替换命令中的star_wars.wav文件。
>
>WAV是最接近无损的音乐格式，所以文件也比较大。



# 广播歌曲：星球大战

```shell
sudo git reset --hard 71e7e23a0e

sox star_wars.wav -r 22050 -c 1 -b 16 -t wav - | sudo ./fm_transmitter -f 100.6 -
```

按`ctrl`+`c`结束广播。



# 广播实时语音

插上USB声卡，在USB声卡的麦克风孔里插入麦克风，运行以下命令，在即可在调频100.6MHz频道广播实时语音，你也可以把这条命令中的100.6改成其它数字，那样就会在新频道上广播：

```shell
arecord -D plughw:1,0 -c1 -d 0 -r 22050 -f S16_LE | sudo ./fm_transmitter -f 100.6 -
```

按`ctrl`+`c`结束广播。



# 扩展应用

用移动电源给树莓派供电，设置开机免密码自动登录和自动运行广播脚本，将整个系统装在书包里，即可实现走到哪里，广播开到哪里（旅游景点、重要会场讲话、窃听器、位置信标）。与无线供电或太阳能相结合，可以实现半永久性的窃听广播站。

例如，大佬做讲座的报告厅人满为患，就可以做一个fm广播站，让堵在门外的人也能听到实时语音。

例如，如果有窃贼或非法入侵者触发了信号（如红外探头、微动开关等），就立刻开启fm广播电台。



# 声明

> 本教程仅供科研与学习交流之用，广播功率很小。如想搭建大功率电台请遵守国家法律法规按正规流程申请备案。
>
> [中华人民共和国无线电管理条例](<http://www.srrc.org.cn//2017/tiaoli/tiaoli.aspx>)<br>
>
> 摘录：
>
> 第五条 国家鼓励、支持对无线电频谱资源的科学技术研究和先进技术的推广应用，提高无线电频谱资源的利用效率。
>
> 第十四条 使用无线电频率应当取得许可，但下列频率除外：
>
> （一）业余无线电台、公众对讲机、制式无线电台使用的频率；



# 扩展阅读与参考文献

> [让树莓派说出自己的ip地址](https://www.cnblogs.com/ma6174/archive/2013/09/29/3345278.html)
>
> [Bilibili视频：【熟肉】教你用树莓派制作可以进行语音直播的FM调频无线电台](https://www.bilibili.com/video/av23299793/?spm_id_from=333.788.videocard.1)

![子豪兄的树莓派系列教程](https://upload-images.jianshu.io/upload_images/13714448-bc64c10051174fde.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![微信扫码支持子豪兄制作树莓派教程](https://upload-images.jianshu.io/upload_images/13714448-4be7dc29e22207b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

![树莓派接线](https://upload-images.jianshu.io/upload_images/13714448-d706c8c62aa45125.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/842/format/webp)

![欢迎加入树莓派全球开源社区](https://upload-images.jianshu.io/upload_images/13714448-9413183a2d79c2a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

