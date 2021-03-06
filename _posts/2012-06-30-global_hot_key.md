---
layout: post
title: 全局快捷键
category: tech
---

曾经有人说过不用鼠标会让你的工作效率提高一倍——他的意思是没有鼠标就不会无聊地去打开网页点点这个，点点那个，时间一会就浪费了。虽然说法很勉强，很偏激(记不住各种快捷键的人没了鼠标会疯掉的)。但是，最近的确我有点讨厌点鼠标了——右手食指尖点地有点疼。我不禁开始怀念起家里Ubuntu的各种快捷键。

Windows下也有各种各样的快捷键。但是无法满足我的需求的是它很少有“全局”的快捷键——那种我在任何时间一摁就能调出我要启动的程序。举个例子：Win(就是键盘上那个画着Windows图标的键)+D算是一个全局的快捷键，任何时候摁它都能立即显示出你的桌面。可是我需要的是一下子就能启动Chrome浏览器，启动Vim，在Windows下该怎么搞呢？

在Ubuntu下这很容易。在Control Center里找键盘快捷键就行了。如下图：

![image](https://public.sn2.livefilestore.com/y1pNfl7QmeC_WDb-xFMhUlbmPZXashQkVYaMPDGEuB9yVj-yPEgf8iuaIJW0ziGqRlktas2Xd1Tlz0rWfIAdSCYQg/lin_hotkey_set.png?psid=1)

下面是我的快捷键设置。Ctrl+2就能启动Chrome，在Ubuntu和Win下面都是一致的。这是我最满意的。

``` php
		Ubuntu			Windows
ctrl+` 		Nautilus		Explorer
ctrl+1 		shell			cmd
ctrl+2 		chrome			同
ctrl+3 		dropbox			同
ctrl+4 		firefox			同
ctrl+5 		gedit			vim
ctrl+6 		calc			同
ctrl+7 					youdao 
ctrl+0 		平铺窗口
ctrl+9 		平铺桌面
ctrl+F11 	窗口变化
alt+F1 		总菜单
```

启动软件现在变轻松了，不用一层一层的去点，不用到桌面上去找图标。关软件呢？一直就很容易啊。Alt+F4，这个几乎已经是通用的“关闭”代名词了。

### 在Windows下实现全局快捷键

微软没给我们提供全局快捷键的设置，那我们只能找第三方程序了。Google之后发现有个叫“Hoekey”的软件很不错，小巧，设置方便。就是它了！

软件的主页在此： "http://www.bcheck.net/apps/hoe.htm":http://www.bcheck.net/apps/hoe.htm

页面上有很多版本，不过貌似还是1.13版好用。 "下载链接":http://www.bcheck.net/apps/HoeKey113.zip

下载解压双击Hoekey.exe 然后设置就行啦。

设置对程序员来说也是很方便的: 用编辑器打开hoekey.ini 看看代码就知道了。

作者用~代表windows键，^代表ctrl键等等，一琢磨便知:-)

把我的设置代码贴一下，仅供参考。

``` php

~N=Run|notepad.exe		; Notepad

^`=Run|explorer.exe %c		; Explorer in current directory

^1=Run|cmd.exe|||%c		; Command shell in current directory

^2=Run|C:\Documents and Settings\azhang2\Local Settings\Application Data\Google\Chrome\Application\chrome.exe	; Chrome

^3=Run|C:\Documents and Settings\azhang2\Application Data\Dropbox\bin\Dropbox.exe		; Dropbox

^4=Run|D:\Program Files\Mozilla Firefox\firefox.exe		; FireFox

^5=Run|E:\My Dropbox\note.txt	; Vim

^6=Run|C:\WINDOWS\system32\calc.exe	; Calculator

^7=Run|D:\Program Files\kuwo\Youdao\Dict4\YodaoDict.exe	; Youdao

^Q=Run|C:\Program Files\Tencent\QQ\Bin\QQ.exe	; QQ

^K=Run|C:\program files\skype\Phone\Skype.exe	; Skype

```

诀窍就是在竖线和分号之后填上你要启动的程序的地址就行了。地址？就去你要启动的程序的图标的右键属性窗口里去找吧。

记得修改完快捷键之后要再点下Edit Config按钮，这样才能立马生效哦。

![image](https://public.sn2.livefilestore.com/y1pwfhqbHIt-DMNBQVWjPQ_VpTuic1ooivpQADfgwYfSrmmEj23uqotkenCIE7-AO1cfmVikWzhWXpAwLhe3IONUg/800-600.a3fe43001e8f76bb8476db89f58c0b36252e8aa6.57dcda.jpg?psid=1)

### 结语

好了，结束！ Enjoy快捷键吧。
