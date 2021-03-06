---
layout: post
title: Windows整点提醒DIY
category: tech
---

### 你需要定时提醒功能吗？

如果对以下几点深有同感：

* 在电脑前常常忘了时间，一回神两个小时已经过去了
* 本来打算随便看看就学习，没想到随便一看又过了一个多小时
* 早就知道看屏幕一小时后要休息眼睛，可是常常忘记了

那么，你就像我一样需要一个报时软件——及时提醒你已经在电脑前待了太长的时间，应该休息调整一下了。

### Windows自已就有这个功能

有定时提醒功能的软件多牛毛，设置和提醒效果也从简单到复杂多种多样。定时是计算机一个再基本不过的功能，那么，我们能不能不安装任何第三方软件，简简单单就能达到达到定时提醒的效果呢？

答案当然是肯定的。今天，我们就在Windows XP系统中实现一下定时提醒的功能。

先来看看实现后的效果： 
![image](https://public.sn2.livefilestore.com/y1pltPnYdZg9WmJ6kjwJ5ZAQ4oAE9CFbcTQ-B-EcI4kvFm-cI4AWU4X8_m5owAfwievXt72MAzv9Bs2qojyIVOCjg/Qtz0Z%20-%20Imgur%20(1).png?psid=1)

够简陋是吧，本文提供的方法只专注于提醒功能与DIY。如果你对界面效果有很高的要求，要花哨，那最好还是找一个第三方软件吧。

### 好吧，在XP上实现！ 

#### 1. 首先确保两个系统服务是设成成开机自动启动的。

打开控制面板=>管理=>服务，设置Task Scheduler和Messenger为自动启动。如果这两个服务目前是关闭的，手动把它们启动。

#### 2. 创建一个生成弹出窗口的脚本。

新建一个文本文件，复制下面的代码进去，然后保存为后缀名为bat的文件，取名为timer.bat。这就是我们"定时提醒软件"的程序界面。:-)

``` php
@echo off
for /f %%i in ('time /t') do set a=%%i

rem change you computer name below
net send YOURCOMPUTERNAME NOW is %a%, STOP and TAKE A BREAK. 
```

#### 3. 找到你的计算机名。

右键桌面上的'我的电脑'，点击'属性'，如下图所示，红圈处就是你的电脑名字。

把你的计算机名复制下来，替换掉上一步中的YOURCOMPUTERNAME并保存。 
![image](https://public.sn2.livefilestore.com/y1pTTG8kpTlaaGuY8PoqXWaVrGIPswAG6A_kMKEmvhgVsGtm-lxivYyu9yN8kjGbIkO2P7anPA-9qF8NLSyp5vosQ/etZFE%20-%20Imgur.png?psid=1) 

**注意**:如果你的电脑像我一样也处于某个域中，记得拷贝计算机名的时候把域的名去掉。

#### 4. 试验弹出窗口。

双击你新建的文件。此时应该弹出一个告诉你当前时间的窗口(即本文中第一副图的效果)。

如果未成功的话则需要进入DOS命令行里手动运行timer.bat，看看到底它报什么错。开始=>运行=>输入cmd，回车=>定向到timer.bat所在的路径输入timer.bat并回车。

大部分的时候报的都是找不到对应计算机——这是由于计算机名没找到的缘故，再检查一下第3步中的计算机名你写对了吗？

如果报Messenger服务没有启动，那么就按第1步的提示再检查一下服务到底起来了没有。这个弹出窗口其实依赖的就是Windows的Messenger服务。

#### 5. 设置计划任务。

好了，通过写了一个简单的小脚本，我们的弹出窗口已经搞定了。下一步就是让这个小脚本能按照我们的需要定期的自动运行。

这就用到了Windows的另一个服务——Task Scheduler(计划任务)。

我的喜好是每整点和半点的时候提醒我一次：

控制面板=>计划任务: 
![image](https://public.sn2.livefilestore.com/y1pjO9hiILKH4ZgOCcGzhpMSLf_2oPtGgFs1QWAn_CWVePNsuX5tHgaQpVu9FjslZ36W2vS09azflMUEtb1-Ku2cQ/mJHny%20-%20Imgur.png?psid=1)

添加一个新的计划任务，把我们新建的timer.bat添加到新的计划任务中：
![image](https://public.sn2.livefilestore.com/y1p55QP2q1mwFxhhDEI_SUFBvGKYpQ1KCS-3oFoqWqYo7NVJkRZz3UueCF7MYOQVeeR8pRuX8TEA4iurVmuioyP4A/w7cjw%20-%20Imgur.png?psid=1)

给这个计划任务起个名字，我叫它'半点报时'： 
![image](https://public.sn2.livefilestore.com/y1pTTG8kpTlaaHmvdXZqMSIwfO8i6y7oJh4O_4lnFNkKK2UIvLYzogMSX-QOwlRleOqy_xtzz4sps4fXFYNHGYwrw/59gfV%20-%20Imgur.png?psid=1)

设置开始时间与运行频率：

*注意*:开始运行时间一定要选择还未到的时间，如果你选择一个过去的时间(一小时以前或者昨天)这个新的计划任务是不会启动的——Windows没那么智能。

![image](https://public.sn2.livefilestore.com/y1pTTG8kpTlaaFMYr1wXaRL2eBdo_bYgcjEAXb4d_v8oDmmnn9vPnYQ0bPt_BiCtxbxd1pf9MeYEknUUNuZ-vQqFg/iid0I%20-%20Imgur.png?psid=1)

输入管理员密码：设定这个计划任务是以什么身份运行——输入你的Windows登录名和密码。 
![image](https://public.sn2.livefilestore.com/y1pxqA_Xdt4UaOJXmILMhOShjBIvSyqWOQLskU1Ajoy-ym24o2ttNVYgXeQyupB9Dyyc8kYDzo5-KMx0a6zTswp-g/ZGVQd%20-%20Imgur.png?psid=1)

#### 6. 进一步设置频率。

这个时候一个新的计划任务应该是已经建好了，不过还达不到我的要求——半小时运行一次。刚才的设置只是一天运行一次。怎么办呢？

进一步设置，右键'半点报时'=>属性：
![image](https://public.sn2.livefilestore.com/y1p9M-GZFBS5Xy3e1k3MP5wEs42Yuung-JDwuuiDnIhnZgya3HwnYt21GA44Njt5gP1IFRBWzqjxUz8NkxutxBiow/VZZDc%20-%20Imgur.png?psid=1)

选择第二个标签页，并点'高级'，如下图：
![image](https://public.sn2.livefilestore.com/y1p55QP2q1mwFyEnCKhzCLszs4rxVnjHRIzB80YraGiZUAs1IUWcP_h5q9rf47OYK1r-5u6dlh7OB3qwf1IA_oukA/wEdVF%20-%20Imgur.png?psid=1)

*注意*:

* "重复任务"栏里输入你想运行的频率，半小时，1小时，2小时…… 
* 持续时间：这个控制了重复的范围，我希望只要电脑开着就要半小时提醒一次，所以我输入了24小时。如果你并不需要，那么输入你的希望值。

#### 7. 试试能按时提醒了吗？

如果你没耐心等到半点或整点的时候检测那么就把第6步的起始时间和频率改一改，比如把频率改成1分钟一次，起始时间改成1分钟之后，这样一分钟后马上就能知道结果啦！ ^-^

至此，XP里的设置就完成了：
![image](https://public.sn2.livefilestore.com/y1pltPnYdZg9WmJ6kjwJ5ZAQ4oAE9CFbcTQ-B-EcI4kvFm-cI4AWU4X8_m5owAfwievXt72MAzv9Bs2qojyIVOCjg/Qtz0Z%20-%20Imgur%20(1).png?psid=1)

"STOP and TAKE A BREAK"是我自己写给自己的，你可以在timer.bat里想写啥写啥，修改代码就了。

### Win 7 的设置

Win 7和XP原理和设置都是类似，除了有两点变化：

* Messenger服务变成了msg.exe
* 向计算机名发消息变成了向指定用户名发消息

所以timer.bat的内容就变成了：

``` php
@echo off
for /f %%i in ('time /t') do set a=%%i

rem win7 below:
msg.exe Administrator NOW is %a%, TAKE A BREAK. 
```

*注意*:如果你的Win7登录时并不是管理员账号登录那么就把Administrator换成你的用户名

### 结语

电脑消耗了现代人太多的时间，其实，你真的需要在屏幕前花那么多时间吗？即使工作很忙，定时提醒下休息五分钟，同时也让你总结下过去的半小时或一小时自己究竟完成了些什么，是不是可以让你的效率更高呢？

我认为是会的。

当然，不排除过一段时间之后，特别是工作很忙的时候你会对这个弹出来提醒休息的窗口视而不见了，甚至有些厌烦了。但是，也许你真的需要一个在你身边准时地、不厌其烦地提醒你该休息了的忠实仆人。

管理好你的时间！你只需要遵守它！
