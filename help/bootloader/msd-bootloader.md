# Mass Storage Device Bootloader（U盘模式）

基于lufa msd的，这里的U盘模式是指键盘本身虚拟成为一个U盘，不是说刷新固件时需要一个额外U盘。

ydkb.io支持的如下键盘使用了该刷机模式。

| 支持键盘 ||||||
| --- |||||| 
|1800mini|Mater98|Sairo64|X-8086K|
|Duang60|Just60|Just66|Just660|Just68|Pearly|
|ESWN|AKB48|Cod67|Filco104c|
|HHKB BLE|BLE660C|
|U2U Pro|UDock|

<html><div class="hint"> 
<subtitle>提醒：</subtitle>
<ul><li>键盘的U盘模式下显示的两个文件，“键盘名.BIN”和“EEPROM.BIN"，它们只是映射了主控FLASH和EEPROM的内容而“虚拟”出来的文件。</li>
<li>每次重新进入刷机模式时它们的文件日期显示是固定的，不要用文件日期来判断是不是更新成功。</li></ul>
</div></html>


## 刷新出错的处理

把这一条放在最前面。如果刷错固件或者没刷成功的，导致无法再进入刷机模式，特别是双模的键盘，只需要把键盘的电源开关关掉或拔掉电池，然后再重新进入刷机模式，刷好正确的固件即可。


## Windows下刷机方法

刷机的方式基本都一致，一般是按住左上角键或者其他某个指定的键不放（具体看ydkb.io对应键盘里有显示的刷机说明），插入USB进入刷机的U盘模式。再把固件的bin文件（不需要区分大小写）拖到U盘里覆盖原文件即可。


## Mac下刷机方法

<html><div class="attention"> 
<subtitle>重要：</subtitle>
<br>Mac务必严格按照下面步骤，不然可能刷新不成功。
</div></html>

<col_h5>键盘自身进入刷机的U盘模式方法都是相同的，但Mac下复制文件方法不同。</col_h5>

<html>
<two_col>
<div style="float:left;width:48%;">
<col_list>1 先在U盘里删除固件里的"键盘名.bin"这个文件。</col_list>

![](/assets/msd-bootloader-mac01.png?)

<col_list>2 再在废纸篓里也要删除它(对Mac来说这一步非常重要)。</col_list>

![](/assets/msd-bootloader-mac02.png?)
</div>
<div style="float:left;width:3%;">&nbsp;</div>
<div style="float:left;width:48%;">
<col_list>3 将新下载的bin保持文件名与之前删除的bin文件一样，再复制到U盘里(注意先后)。</col_list>

![](/assets/msd-bootloader-mac03.png?)

<col_list>4 待文件复制完成后，右键推出U盘或按Esc退出，刷机完成。</col_list>

<col_list>5 这是针对4的补充：部分比较新的bootloader，在文件复制完后，会自动退出。这时Mac下提示未正确退出之类的是正常现象。</col_list>

<html><div class="hint"> 
<subtitle>提醒：</subtitle>
<br>如果在废纸篓里删除后，复制文件时还是提示空间不足，那么退出刷机模式然后再重新进刷机模式，再重新操作。
</div></html>

</div>
</two_col>
<div style="clear:both;"></div>
</html>


## Linux下刷机方法

<html><div class="hint"> 
<subtitle>提醒：</subtitle>
<br>下面的方法仅测试了Ubuntu 19.04。其他的Linux版本可能会不同。所以，需要刷固件的时候，建议还是去win下刷最稳妥。
</div></html>

这个还比较奇特，我这里以Ubuntu 19.04做的测试。首先不能像mac那样直接操作u盘。用命令行，如下图，要注意文件的大小写也要对应，而且这个命令要连续运行两次，我试过Ubuntu 19.04只运行一次的时候，退出U盘，按键并没有变，运行两次就都成功。如果还有其他的变动我再补充。

<div style="width: 600px">

![](/assets/msd-bootloader-linux01.png?600)
</div>


## 如果反复进入U盘模式

如果出现这个问题，多半是因为下载的bin文件不对。可以随便用一个txt文件编辑器打开bin文件，看看内容是不是空的。或者用16进制查看器，查看文件前面是不是全是FFFF。

解决方法是多刷新（Ctrl+F5）几次页面重新下载固件，然后重新刷入。


## 如果提醒下载文件有错

如果下载时遇到提醒“下载文件有错，Shift+F5刷新页面后重试”，就多用Shift+F5刷新几次页面，或者进Chrome的隐身模式下载一下。在下载文件前加入了一个简单的检测机制，以避免下载到的是空文件从而引起“反复进入U盘模式”的问题。


## 如果无法覆盖bin文件
如果直接覆盖bin提示空间不足，打开资源管理器显示隐藏文件，看看这个U盘里除了xxx.bin和eeprom.bin外，是否还包含了其他文件，如果电脑本身有中毒为新u盘写入了文件占用了空间，则替换xxx.bin时就会提醒空间不足，造成无法替换。

