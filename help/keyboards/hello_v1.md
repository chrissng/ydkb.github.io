# Hello Keyboard

从开始做HHKB BLE的主控开始，有一年多的时间里，我一直主力键盘是HHKB，喜欢它的手感，还有它纯粹的感觉，没有RGB，就安安静静的使用就好。

原HHKB Pro2经过改装后，重量也就500多g，很便携，但是我个人对便携并没有需求。有不同地方都需要使用同样的设备时，我一般会选择各备一套。

我感受到了铝坨坨的召唤，怡科外设(KBDFans)正好也要出HHKB的替换外壳，然后一经商量，就有了这么一个产品。除了改装HHKB用外，还可配套其他的轴板，我将它取名叫了Hello Keyboard。

---

## 主要介绍
Hello Keyboard其实很单纯，也没有RGB，一方面，它可以将原来的HHKB Pro2经过改装，成为一个双模的铝壳静电容键盘；另一方面它还支持其他机械轴体，标准的MX轴体当然是少不了的。

在改装HHKB的同时，将轴心换成了十字的，这样可以兼容更多的键帽，同时，空格使用的是6.25u的，而非6u。

就功能而言，部分与HHKB BLE主控功能相同，但也有一些变化。

固件的更新记录可见：[[changelog:hello_v1|Hello v1固件更新记录]]。


---

## 蓝牙配对

蓝牙配对主要参看，[[:ble-series|BLE双模使用]]

保持底部开关是打开的，在Hello v1里，此开关是电池的供电开关，同时也是蓝牙的开关。

不需要单独启用配对模式，只要蓝牙处于未连接并且可发现状态，就可以配对。mac和ios的搜不到在上面文档里也有写处理方法，另外出现连接异常时，也有处理方法。

---
## 固件设置

固件基于tmk，在https://ydkb.io上进行设置，常见的功能均可通过网页进行设置。  

---

## 固件更新

可以直接看这部分。[[bootloader:msd-bootloader|Mass Storage Device Bootloader（U盘模式）]]

在进入Bootloader后，的指示灯三个会闪，在刷入文件时第三个指示灯会快速闪烁。

补充说明是除了左上角键（一般是ESC）插线可以进入刷机模式外，还可以使用**灯光和增强功能**里的<html><button style=" text-align: center; line-height: 19px; width: 46px; height: 42px; font-size:12px">Reset</button></html>，为了防止误按，当与左Ctrl一起按的时候，也就是左Ctrl+Reset，可以直接跳到刷机模式，不用拔线再重插。还可以按 **LShift+RShift+B** 后键盘会重启，这时立即按住Esc不入，也可以进入刷机模式。

---

## 指示灯说明以及节能

除了上面说的BL模式下指示灯作用外。普通的功能可以通过LEDMAP（[[features:ledmap|LEDMAP]]）定义三个指示灯的功能。指示灯仅在键盘未节能时亮起，建议不要设置需要经常常亮的指示，每颗指示灯一直亮起增加的耗电，会减少键盘的续航。

LEDMAP的默认定义，正面，LED1(默认红灯)为CapsLock，LED2(默认黄或白灯)为层1指示（按Fn时会亮），LED3（默认绿灯）为层2指示。

除了设定的LEDMAP外，其他的指示功能总结如下，其他的指示都是指示灯会闪。
^ 指示灯 ^ 指示内容 ^
^ 三个灯一直闪 | 刷机模式 |
^ 使用键盘时三灯闪，不使用时灭 | 低电量指示 |
^ 仅LED3较快闪 | 蓝牙未连接或连接中 |
^ LED2和LED3较慢闪 | 蓝牙已连接 |


除了定义的功能外，还有特殊作用。
  - 当进入Lock Mode时，三个灯先是同时亮时，然后从右往左依次熄灭。 
  - 当从二级节能唤醒时，三个指示灯会同时亮一下，然后再灭。
  - 电池电量低时，在使用键盘时三个指示灯会同时闪。报电量不足后依然还可以使用两三天。
  - 电池电量极低时，在使用键盘时三个指示灯会同时快闪，每秒闪3下左右。此时建议尽快充电。

然后关于节能模式的说明：
  - 键盘闲置3秒没按任何按键后，进入一级节能，此时每30ms再重新检查一次矩阵有无按键，有按键就退出一级节能，这个唤醒过程很快。
  - 键盘如果90秒蓝牙未连接，或者闲置时间超过2.5小时，这时蓝牙会关闭并断开，进入二级节能。长按任意键3到5秒可以唤醒。
  - 使用Lock Mode，会直接进入二级节能，与2的区别是，这个模式下，只能同时长按F和J唤醒，不能长按任意键唤醒。

蓝牙连接状态，同时按下 **左Shift+右Shift+S** 切换蓝牙连接状态指示开关：
  - **LED3快递闪烁**，闪的过程中，亮和灭时间相当，此时蓝牙未连接
  - **LED2和LED3较慢闪烁**，闪的过程中，亮的时间比灭的时间明显的更长，此时蓝牙已连接


二级节能的功耗是很低的，如果不是特别长期的不用，比如只是第二天不用，可以直接让键盘自己进入二级节能或者直接手动进入Lock Mode（后者更适合放包里，防止意外唤醒）。


---

## 异常处理
工作时如果出现什么异常，最快速的方法是重新插一下usb线或是拔线后重新开关一下键盘开关。

如果有配对后使用的问题，只要有线还能使用，那么，首先用文字输出电量功能，看一下输出的数字是多少。如果是44或45，可能需要[[ble-series:reset-ble|重置蓝牙]]。

大部分使用的问题参看BLE Series的部分。

遇到bug可以通过群里联系等方式报给我。

---