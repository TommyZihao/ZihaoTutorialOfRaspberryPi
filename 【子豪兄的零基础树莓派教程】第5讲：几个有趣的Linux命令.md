# 【子豪兄的零基础树莓派教程】第5讲：23个有趣的Linux命令

>【子豪兄的零基础树莓派教程】第5讲：
>
>本文介绍了23个有趣的Linux命令，向新手介绍了Linux命令行基本知识与“管道”的概念。
>
>这些命令可以在树莓派和Ubuntu系统上运行，最后一条命令还可以在Windows的DOS命令行中运行。
>
>源代码、更新、勘误，请看本教程Github代码仓库：
>https://github.com/TommyZihao/ZihaoTutorialOfRaspberryPi
>
>[同济大学开源镜像站](https://mirrors.tongji.edu.cn/)



## 1、黑客帝国高大上的字节流效果cmatrix

在命令行界面输入

```shell
sudo apt-get install cmatrix
```

- sudo：获取管理员root权限
- apt-get：Linux操作系统的发行版之一Debian系统的包管理器
- install：使用apt-get包管理器安装
- cmatrix：软件名字

然后在命令行界面输入`cmatrix`，回车，即可看到效果。

按`ctrl`+`c`退出。



> 在《黑客帝国》电影里的字节流其实是该片美术指导Simon Whitley的日本妻子菜谱上的片假名。

![img](http://5b0988e595225.cdn.sohucs.com/images/20171025/910ced0b04f643fa98b00bd343d26724.jpeg)



## 2、追逐鼠标的小猫oneko

在桌面的命令行界面输入

```shell
sudo apt-get install oneko
```

然后输入`oneko`，即可看到效果

> 注意，本命令只能在桌面所在的命令行界面输入，在远程ssh界面会显示“oneko:Can't open display”

按`ctrl`+`c`退出。





## 3、燃起字符串大火aafire

在命令行界面输入

```shell
sudo apt-get install libaa-bin  
```

然后输入 `aafire`，即可看到效果

按`ctrl`+`c`退出。



## 4、火车

在命令行界面输入

```shell
sudo apt-get install sl
```

然后输入 `sl`，即可看到效果。

输入`sl-h`可以看到彩蛋（没有空格）



## 5、大眼睛

在命令行界面输入

```shell
sudo apt-get install xeyes
```

然后输入 `xeyes`，即可看到效果：一双紧盯着鼠标所在位置的大眼睛。

按`ctrl`+`c`退出。



## 6、艺术字生成器toilet

在命令行界面输入

```shell
sudo apt-get install toilet
```

然后输入下面任意一行命令，通过在命令中加-f更换字体或滤镜，你可以把命令里的`shumeipai`换成你想要转换的字符。

案例1 

```shell
toilet shumeipai
```

案例2 双色字：

```shell
toilet -f mono12 -F metal Shumeipai
```

案例3 彩色字：

```shell
toilet -f mono12 -F gay Shumeipai
```

输入`man toilet`查看更多帮助，按`q`退出。



## 7、艺术字生成器figlet

在命令行界面输入

```shell
sudo apt-get install figlet
```

然后输入下面任意一行命令，通过在命令中加-f更换字体或滤镜，你可以把命令里的`shumeipai`换成你想要转换的字符。

案例1 

```shell
figlet shumeipai
```

案例2 双色字：

```shell
toilet -f mono12 -F metal Shumeipai
```

案例3 彩色字：

```shell
toilet -f mono12 -F gay Shumeipai
```

输入`man toilet`查看更多帮助，按`q`退出。



## 8、字符串视频

在命令行界面输入

```shell
sudo apt-get install xeyes
```

然后输入 `bb`，选择`y`加音乐，选择`8`继续，即可看到一段用字符串制作的视频，讲述了视频作者的生涯和使用Linux操作系统的历程，这段视频制作于1997年，基于AAlib平台制作。

按`ctrl`+`c`退出。



## 9、输出名人名言、古诗词

在命令行界面输入

```shell
sudo apt-get install fortune
sudo apt-get install fortune-zh
```

然后输入 `fortune`，即可看到效果。



## 10、超级牛力

在Ubuntu和Debian上，apt-get包管理器内嵌着一个彩蛋。
如果你在命令行界面输入

```shell
apt-get help
```

在最后一行能找到

This APT has Super Cow Powers.

则说明你的系统可以运行这个菜单

在命令行界面输入

```shell
apt-get moo
```

即可看到这个彩蛋。



## 11、会说话的牛

在命令行界面输入

```shell
sudo apt-get install cowsay
```

然后输入 `cowsay “Hello Tongji Univerisity”`，

只需用 `-l`参数就能看到它能提供的所有动物。

```shell
cowsay -l
```

会输出如下人物，你可以通过`-f`参数加人物名字来更换说话人物：

```shell
Cow files in /usr/share/cowsay/cows:
apt beavis.zen bong bud-frogs bunny calvin cheese cock cower daemon default
dragon dragon-and-cow duck elephant elephant-in-snake eyes flaming-sheep
ghostbusters gnu head-in hellokitty kiss kitty koala kosh luke-koala
mech-and-cow meow milk moofasa moose mutilated pony pony-smaller ren sheep
skeleton snowman sodomized-sheep stegosaurus stimpy suse three-eyes turkey
turtle tux unipony unipony-smaller vader vader-koala www
```

比如更换成hellokitty：

```shell
cowsay -f hellokitty 'Hello Tongji Univerisity'
```

也可以利用管道命令，将fortune生成的名人名言在cowsay中输出

```shell
fortune | cowsay
```

加个颜色

```shell
sudo apt install lolcat
```

再利用管道命令

```shell
fortune | cowsay | lolcat
```

或者输入以下命令，让恐龙大哥说话：

```shell
echo 'Hello Tongji University' | cowsay -f stegosaurus
```







## 12、会说话的牛2

> 注意，本命令只能在桌面所在的命令行界面输入，在远程ssh命令行界面输入会显示“Can't open display”

在命令行界面输入

```shell
sudo apt-get install xcowsay
```

然后输入 `xcowsay “Hello Tongji Univerisity”`



## 13、日历

在命令行界面输入

```shell
cal 10 2018
```

即可看到2018年10月的日历。

有趣的是，如果你输入

```shell
cal 9 1752
```

你会发现这个月少了11天，这是因为当时大英帝国美洲殖民地的历法从凯撒历法换成了格里高利历法，凯撒历法要迟11天，所以这11天成了日历上的空白期。

[1752年9月为什么少了11天？](http://blog.sina.com.cn/s/blog_8713f2c501013md6.html)



## 14、yes命令

在命令行界面输入

```shell
yes Tongji University
```

就会看到无穷无尽输出的Tongji University

按`ctrl`+`c`退出。



## 15、分解因数

在命令行界面输入

```shell
factor 60
```

即可看到60的分解质因数的结果



## 16、反转字符命令rev

在命令行中输入`rev`，打开rev界面，然后输入任意字符，比如

```shell
I am a student in Tongji Univerisity
```

按回车，即可看到字符反转之后的结果

按`ctrl`+`c`退出rev界面回到命令行界面。

```shell
echo "I am a student in Tongji Univerisity" | rev
```

将一句话中所有单词的顺序反转,但在单词内部字母顺序不变

```shell
echo "I am a student" | rev | tr ' ' '\n' | tac | tr '\n' ' '| rev
```





## 17、screenfetch:显示系统、主题信息

```shell
sudo apt install screenfetch
screenfetch
```



## 18、linux各版本logo图片及系统信息

```shell
sudo apt install linuxlogo
linux_logo
```

循环打印图标

```shell
for i in {1..30};do linux_logo -f -L $i;sleep 2;done
```



## 19、图片转字符串

```shell
sudo apt-get install aview
sudo apt-get install imagemagick

wget http://labfile.oss.aliyuncs.com/courses/1/Linus.png

asciiview Linus.png
```







## 20、box命令：在输入的文本或者代码周围框上各种ASCII 艺术画。

```shell
sudo apt-get install boxes
echo "Tongji Univerisity" | boxes
echo "Tongji Univerisity" | boxes -d dog
```







## 21、pv命令：字幕一个个匀速显示出来

```shell
sudo apt-get install pv
echo "Tongji Opensource" | pv -qL 10
```





## 22、从删库的跑路 sudo rm -rf /*

![sudo rm -rf /](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539792611926&di=a261ba9fadfa7ba727ef2a7c724016e1&imgtype=0&src=http%3A%2F%2Fi0.hdslb.com%2Fbfs%2Farchive%2Fb6d4f8aa58841f6e8674c3bd46126e5f8ad5fc7f.jpg)

> 友情提示：千万不要轻易尝试这个命令，特别是在运行有网站服务器、数据库的Linux主机上

```shell
sudo rm -rf /*
```

- sudo：获取root管理员权限
- rm：remove，即删除
- -rf：r表示递归删除，即删除所有的子目录，f表示不需要再进行确认
- /：home目录
- *：所有文件

**也就是说，这条命令是删除这台Linux主机上的所有文件，甚至包括开机文件**

关于这条命令的一些有趣的图片：

![删库大爆炸](https://upload-images.jianshu.io/upload_images/13714448-057901398c109d38.GIF?imageMogr2/auto-orient/strip)

![从删库到跑路1](https://upload-images.jianshu.io/upload_images/13714448-9108c4583143f501.GIF?imageMogr2/auto-orient/strip)

![数据库删了肯定要跑路啊](https://upload-images.jianshu.io/upload_images/13714448-e42e61a486b7d1fd.GIF?imageMogr2/auto-orient/strip)

![从删库到跑路2](https://upload-images.jianshu.io/upload_images/13714448-77ce9a2551b16ad4.GIF?imageMogr2/auto-orient/strip)





## 23、播放星球大战

这条命令在你自己的笔记本上都可以运行

1、打开控制面板，找到”启动或关闭Windows功能“，然后打开Telnet客户端。

![控制面板](https://upload-images.jianshu.io/upload_images/13714448-e13443f55165768d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![打开Telnet应用](https://upload-images.jianshu.io/upload_images/13714448-98d0012f082f5cc2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



2、用管理员模式打开DOS命令行界面，输入以下命令，回车。

```shell
telnet towel.blinkenlights.nl
```

![字符串星球大战](https://upload-images.jianshu.io/upload_images/13714448-e03931d0461838a7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)








![](https://upload-images.jianshu.io/upload_images/13714448-1c1f91c8b56023a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





## 扩展阅读与参考文献

> [10个非常有趣的Linux命令](https://www.cnblogs.com/1394htw/p/6358737.html?utm_source=itdadao&utm_medium=referral)
>
> [超有趣的几个Linux命令，你都用过吗？](https://www.cnblogs.com/1394htw/p/6358737.html?utm_source=itdadao&utm_medium=referral)
>
> [Linux中管道命令的用法](https://blog.csdn.net/tq384998430/article/details/54925742)
>
> [FIGlet初识](https://aotu.io/notes/2016/11/22/figlet/)
>
> [fortune中文格言库](https://github.com/ruanyf/fortunes)
>
> [阮一峰的网络日志：fortune 命令简介](http://www.ruanyifeng.com/blog/2015/04/fortune.html)
>
> [1752年9月为什么少了11天？](http://blog.sina.com.cn/s/blog_8713f2c501013md6.html)
>
> [Linux 奇技淫巧](https://www.cnblogs.com/Nice-Boy/p/6091307.html)
>
> [Shell常识--基本函数和简单命令rev--总结自《Linux Shell 脚本攻略》](https://blog.csdn.net/jsjxy2009/article/details/39207595)
>
> [意想不到的有趣linux命令18个，玩得溜](https://blog.csdn.net/qq_41741971/article/details/82053290)
>
> [apt 和 apt-get的区别](https://blog.csdn.net/liudsl/article/details/79200134)
>
> [启用Windows中的Telnet功能一起看DOS版星球大战](https://blog.csdn.net/crazygolf/article/details/48383869/)

![树莓派接线](https://projects-static.raspberrypi.org/projects/raspberry-pi-getting-started/13aeb423985e6bacd5d798f5f206a644b7c250a3/en/images/pi-plug-in.gif)

![欢迎加入树莓派全球开源社区](https://upload-images.jianshu.io/upload_images/13714448-9413183a2d79c2a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
