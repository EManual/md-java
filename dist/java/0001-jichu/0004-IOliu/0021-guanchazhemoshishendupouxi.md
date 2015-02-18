回顾前面所讲内容，抛出一个问题：在Java的AWT或者SWing的GUI编程中，为什么我们对一个按钮关联一个监听器，当我们点击按钮的时候，监听器中的方法就会自动被执行呢？首先可以确定的是根本没有自动的概念，所谓的自动无非就是Java底层中的某一种机制促使这种现象发生，在外面看来像是实现了自动执行的感觉。这就引入了观察者模式，观察者模式在Java中的地位是及其重要的。在讲观察者模式之前，我们要有这样的一个概念，监听器中的方法是按钮去执行的。
* 1、观察者模式(Observer)
1)观察者模式定义了一种一对多的依赖关系[1个按钮，多个监听器]，让多个观察者对象同时监听某一个主题对象[多个监听器同时观察按钮的变化]。这个主题对象在状态上发生变化时[当按钮被点击的时候]，会通知所有观察者对象，让他们能够自动更新自己。[这些监听器中的方法自动得到调用了]
2)观察者模式的组成
(1)抽象主题角色：把所有对观察者对象的引用保存在一个集合中，每个抽象主题角色都可以有任意数量的观察者。抽象主题提供一个接口，可以增加和删除观察者角色。一般用一个抽象类或接口来实现。
(2)具体主题角色：在具体主题内部状态改变时，给所有登记过的观察者发出通知。具体主题角色通常用一个子类实现。[在前面所讲中Button就是一个主题角色]
(3)抽象观察者角色：为所有具体的观察者定义一个接口，在得到主题的通知时更新自己。
(4)具体观察者角色：该角色实现抽象观察者角色所要求的更新接口，以便使本身的状态与主题的状态相协调。如果需要，具体观察者角色可以保存一个指向具体主题角色的引用。通常用一个子类实现
* 2、实现自己的观察者模式
1)抽象主题角色：
```java  
package com.ahuier.observer;
/*  
	//增加一个观察者
	//删除一个观察者
	//通知一个观察者,有什么事情发生通知观察者,会把信息传递给观察者，可以接受一个Object类型参数，这边直接用字符串类型
}
```
2)抽象观察者角色
```java   
	//当抽象主题角色通知发生时，接受主题的通知时更新自己
}
```
3)具体的主题角色
```java  
package com.ahuier.observer;
import java.util.ArrayList;  
/*
public class ConcreteWatched implements Watched {
	//定义一个集合用于承载观察我的观察者
	@Override
		list.add(watcher);
	}

	@Override
		list.remove(watcher);
	}
	/*
		for(Watcher watcher : list){
			watcher.update(str);
		}
	}
}
```
4)具体观察者角色
```java  
/*  
 * 具体的观察者角色    
 * 相当与我们自己定义的Listener一样   
 */  
public class ConcreteWatcher implements Watcher {
	@Override
		System.out.println(str);
	}
}
```
5)定义一个测试类
```java  
package com.ahuier.observer;
/*  
public class Test {
	public static void main(String[] args) {
		//定义一个女孩被很多人观察,相当于一个按钮
		//watcher1相当于一个监听器
		Watcher watcher2 = new ConcreteWatcher(); //观察者2
		Watcher watcher3 = new ConcreteWatcher(); //观察者3
		
		//将这些观察者添加到集合中去，相当于注册一个监听器
		girl.addWatcher(watcher2);
		girl.addWatcher(watcher3);
		//向所有观察者发出通知，我很开心.这个操作相当与点击了按钮
		//删除第二个观察者，并再一次发出通知
		girl.notifyWatchers("不爽");
		
	}
}
```
编译执行结果：
```java  
我很开心
我很开心
我很开心
不爽
不爽
```
【说明】：将这个机制对比之前学习过的AWT中的程序，同时查看Button源代码如下所示，可以发现它们的机制是一样的：
```java  
protected void processActionEvent(ActionEvent e) {
	ActionListener listener = actionListener;
	if (listener != null) {
		listener.actionPerformed(e);
	}
}
```
从这段代码可以看出来，监听器中的方法是由Button来调用的，也就是由观察者的方法是由主题去调用的。
这个观察者模式如下图所示：
  