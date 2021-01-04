# 设置默认层

设置一个层为默认层，默认层就是指一直开启的层，不能被关闭。

这里以Staryu的设置为例子。一共设置了4层，层0的右上角按键是 **默认层1**，即将层1设置为默认层，层1的这个键则是 **默认层2**，层2的这个键则是 **默认层3**，层3的这个键则是 **默认层0**。整体实现的效果就是每按一次这个键，就将下一层设置为默认层，按键就切换一次，最后在层3的时候又将层0设置为默认，一个循环。

<div style="width: 500px">

![](/assets/default-layer-set-01.png?500)

![](/assets/default-layer-set-02.png?500)

![](/assets/default-layer-set-03.png?500)

![](/assets/default-layer-set-04.png?500)
</div>
