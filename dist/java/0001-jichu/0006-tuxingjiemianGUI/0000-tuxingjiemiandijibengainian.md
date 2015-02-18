1) AWT（Abstract Window Toolkit），抽象窗口工具集，第一代的Java GUI组件，是重量级的。 
2) Swing，不依赖于底层细节，轻量级的组件。
GUI全称是Graphical User Interface，即图形用户界面。根据作用GUI组件可分为基本组件和容器。组件又称构件，诸如按钮、文本框之类的图形界面元素，容器其实是一种比较特殊的组件，可以容纳其它组件，如窗口、对话框等，所有的容器类都是java.awt.Container的直接或间接子类。
AWT提供基本的GUI组件，用在所有的Java applets[applets已经很少用了]及应用程序中
1、具有可以扩展的超类，它们的属性是继承的
2、确保显示在屏幕上的每个GUI组件都是抽象类组件的子类
3、Container[容器，容器本身也可以看做是一个组件]，它是Component的一个子类，而且包括两个主要子类
A：Panel  [面板]
B：window [窗口]
SUN公司提供的用于图形界面编程(GUI)的类库。基本的AWT库处理用户界面元素的方法是把这些元素的创建和行为委托给每个目标平台上（Windows、Unix、Macintosh等）的本地GUI工具进行处理。例如：如果我们使用AWT在一个Java窗口中放置一个按钮，那么实际上使用的是一个具有本地外观和感觉的按钮。这样，从理论上来说，我们所编写的图形界面程序能运行在任何平台上，做到了图形界面程序的跨平台运行。