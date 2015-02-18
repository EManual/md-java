Java中内存分为：
栈：存放简单数据类型变量(值和变量名都存在栈中)，存放引用数据类型的变量名以及它所指向的实例的首地址。
堆：存放引用数据类型的实例。
* Java的垃圾回收
由一个后台线程gc进行垃圾回收。
虚拟机判定内存不够的时候会中断代码的运行，这时候gc才进行垃圾回收。
缺点：不能够精确的去回收内存。
```java  
	java.lang.System.gc();	
```
上面代码会建议系统回收内存，但系统不一定回应，会先去看内存是否够用，够用则不予理睬，不够用才会去进行垃圾回收。
* 内存中什么算是垃圾？
不在被引用的对象(局部变量，没有指针指向的)