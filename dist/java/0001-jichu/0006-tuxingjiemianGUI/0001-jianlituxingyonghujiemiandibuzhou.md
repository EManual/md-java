* 建立图形用户界面
Container：Container的两个主要类型是Window和Panel
1) Window是Java.awt.Window的对象
(1) Window是java.awt.Window的对象。Window是显示屏上独立的本机窗口，它独立于其它容器。
(2)Window有两种形式：Frame(框架)和Dialog（对话框）。Frame和Dialog是Window的子类。Frame是一个带有标题和缩放角的窗口。对话框没有菜单条。尽管它能移动，但它不能缩放。
2) Panel是Java.awt.Panel的对象
(1)Panel是Java.awt.Panel的对象。Panel包含在另一个容器中，或是在Web浏览器的窗口中。Panel确定一个四边形，其它组件可以放入其中。Panel必须放在Window之中（或Window的子类中）以便能显示出来。
(2)注：容器不但能容纳组件，还能容纳其它容器，这一事实对于建立复杂的布局是关键的，也是基本的。
* 定位组件
1)容器里的组件的位置和大小是由布局管理器决定的。
2)可以通过停用布局管理器来控制组件的大小或位置。
3)然后必须用组件上的setLocation()[设置位置]，setSize()[设置大小]，或setBounds()[设置边框]来定位它们在容器里的位置
4)容器里的组件的位置和大小是由布局管理器决定的。容器对布局管理器的特定实例保持一个引用。当容器需要定位一个组件时，它将调用布局管理器来做。当决定一个组件的大小时，同样如此。布局管理器完全控制容器内的所有组件。它负责计算并定义上下文中对象在实际屏幕中所需的大小。
* 组件大小
1)因为布局管理器负责容器里的组件的位置和大小，因此不需要总是自己去设定组件的大小或位置。
2)如果必须控制组件的大小或位置，而使用标准布局管理器做不到，那就可能通过将下述方法调用发送到容器中来中止布局管理器：
setLayout(null);
3)做完这一步，必须对所有的组件使用setLocation(),setSize()或setBounds()，来将它们定位在容器中。请注意，由于窗口系统和字体大小之间的不同，这种办法将导致从属于平台的布局。更好的途径是创建布局管理器的新子类