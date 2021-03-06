---
layout: post
title: Linux整点提醒
category: tech
---

### Linux下的整点提醒

"上篇文章":http://mohaha.tk/tech/2012/04/29/windows_xp_DIY_timer_clock.html 写了Windows XP下面的整点提醒，貌似没有人感兴趣嘛……不过我还是把在Linux下的方法也写出来吧。说不定会对有些人有点用。

我在家用Ubuntu(Gnome桌面)比较多，所以就以Ubuntu为例来说明吧。下图先来一张实现后的效果：
![image](https://public.sn2.livefilestore.com/y1pD1YCQt-Iin7rGEt3LFDam0mXcmzmZJaM-kTeFlUCz8n15FtoOpt5_VkuxsbSqo_OlqPF9eMx2udQtSMF8IVQCw/aUTFB%20-%20Imgur.png?psid=1)

### 开始实现！ 

#### 1. 安装zenity

zenity是Gnome下面一个产生对话框、进度条等等交互效果的程序。我打算用这个小程序来实现我们的弹出对话框(什么？你没用Gnome?那就麻烦你不用往下看了，找个你的桌面环境下的对应程序吧……)

只要装了Gnome一般zenity都是已经安装在里面的。如果不放心可以手动安装下。

``` php
sudo apt-get install zenity
```

测试一下你的zenity能用不？运行以下命令：

``` php
zenity --question --text="Are you sure you wish to proceed?"
```

弹出一个要你选择yes/no的对话框没？出来的话就继续！

#### 2. 实现提醒界面

新建一个timer.sh，复制下面的代码进去。

``` php
export DISPLAY=:0.0
now=$(date +%T)
zenity --info --text "It's $now now. \n\nThink about the past 30 mins." --title "Take a BREAK"
```

export DISPLAY=:0.0 这句话很重要。crontab本来只是用来运行无GUI程序的，就是没有界面的那种。只有加了这条，crontab才能在运行上面的脚本时弹一个框子来。不然的话它确实是运行过了，但是你在界面上看不到提示，白忙活了！

#### 3. 设置crontab

crontab就是linux下的计划任务。有过Linux服务端开发的人一定不会陌生。Ubuntu下设置crontab很容易，输入

``` php
crontab -e
```

再添加两条crontab记录，我的是这样的：

``` php
# m h  dom mon dow   command
30 * * * * /home/allen/Dropbox/timer/timer.sh
00 * * * * /home/allen/Dropbox/timer/timer.sh
```

最好把写上脚本的绝对路径。保存并退出。

#### 4. That's it!

crontab让linux下设置定时任务比Windows简单了许多。如果你的crontab设置后脚本却并没有正常运行——有可能是你的crontab没开启？

测试crontab的方法就是给它加几个简单的任务——每两分钟让Linux在指定目录执行一个生成新文本的任务。如果成功生成的话就说明crontab是正常的。再不行可能还要重启crontab服务。

### 结语

嗯，好了，结束！

下面列出来一些参考资料。

1. "zenity manual":http://library.gnome.org/users/zenity/3.1/zenity.html
2. "Ubuntu 使用crontab定时任务":http://blog.csdn.net/mydeman/article/details/3727060
3. "crontab: How to run GUI programs with cron":http://ubuntuforums.org/archive/index.php/t-185993.html
