日期时间类型的数据也是经常用到的，比如员工出生日期、结账日期、入库日期等等，而且经常需要对这些数据进行处理，比如检索所有超过保质期的商品、将结账日期向后延迟3天、检索所有每个月18日的入库记录，进行这些处理就需要使用日期时间函数。SQL中提供了丰富的日期时间函数用于完成这些功能，本节将对这些日期时间函数进行详细讲解。
* 日期、时间、日期时间与时间戳
根据表示的类型、精度的不同，数据库中的日期时间数据类型分为日期、时间、日期时间以及时间戳四种类型。
日期类型是用来表示“年-月-日”信息的数据类型，其精度精确到“日”，其中包含了年、月、日三个信息，比如“2008-08-08”。日期类型可以用来表示“北京奥运会开幕式日期”、“王小明的出生年月日”等信息，但是无法表示“最近一次迟到的时间”、“徐总抵京时间”等精确到小时甚至分秒的数据。在数据库中，一般用Date来表示日期类型。
时间类型是用来表示“小时:分:秒”信息的数据类型，其精度精确到“秒”，其中包含了小时、分、秒三个信息，比如“19:00:00”。时间类型可以用来表示“每天《新闻联播》的播出时间”、“每天的下班时间”等信息，但是无法表示“卢沟桥事变爆发日期”、“上次结账时间”等包含“年-月-日”等信息的数据。在数据库中，一般用Time来表示时间类型。
日期时间类型是用来表示“年-月-日小时:分:秒”信息的数据类型，其精度精确到“秒”，其中包含了年、月、日、小时、分、秒六个信息，比如“2008-08-08 08:00:00”。日期时间类型可以用来表示“北京奥运会开幕式准确时间”、“上次迟到时间”等信息。在数据库中，一般用DateTime来表示日期时间类型。
日期时间类型的精度精确到“秒”，这在一些情况下能够满足基本的要求，但是对于精度要求更加高的日期时间信息则无法表示，比如“刘翔跑到终点的时间”、“货物A经过射频识别器的时间”等更高精度要求的信息。数据库中提供了时间戳类型用于表示这些对精度要求更加高的场合。时间戳类型还可以用于标记表中数据的版本信息，比如我们想区分表中两条记录插入表中的先后顺序，由于数据库操作速度非常快，如果用DateTime 类型记录输入插入时间的话，若两条记录插入的时间间隔非常短的话是无法区分它们的，这时就可以使用时间戳类型。在有的数据库系统中，如果对数据表中的记录进行了更新的话，数据库系统会自动更新其中的时间戳字段的值。数据库中，一般用TimeStamp来表示日期时间类型。
不同的数据库系统对日期、时间、日期时间与时间戳等数据类型的支持差异性非常大，有的数据类型在有的数据库系统中不被支持，而有的数据类型的表示精度则和其类型名称所暗示的精度不同，比如MSSQLServer中不支持Time类型、Oracle中的Date类型中包含时间信息。数据库中的日期时间函数对这些类型的支持差别是非常小的，因此在一般情况下我们将这些类型统一称为“日期时间类型”。
* 主流数据库系统中日期时间类型的表示方式
在MYSQL、MSSQLServer和DB2中可以用字符串来表示日期时间类型，数据库系统会自动在内部将它们转换为日期时间类型，比如“"2008-08-08"”、“2008-08-08 08:00:00”、“08:00:00” 、“2008-08-08 08:00:00.000000”等。在Oracle中以字符串表示的数据是不能自动转换为日期时间类型的，必须使用TO_DATE()函数来手动将字符串转换为日期时间类型的，比如TO_DATE("2008-08-08","YYYY-MM-DD HH24:MI:SS") 、TO_DATE("2008-08-08 08:00:00", "YYYY-MM-DD HH24:MI:SS")、TO_DATE("08:00:00", "YYYY-MM-DD HH24:MI:SS")等。
* 取得当前日期时间
在系统中经常需要使用当前日期时间进行处理，比如将“入库时间”字段设定为当前日期时间，在SQL中提供了取得当前日期时间的方式，不过各个数据库中的实现方式各不相同。
* MYSQL
MYSQL中提供了NOW()函数用于取得当前的日期时间，NOW()函数还有SYSDATE()、CURRENT_TIMESTAMP等别名。如下：
```java  
SELECT NOW(),SYSDATE(),CURRENT_TIMESTAMP
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
NOW() SYSDATE() CURRENT_TIMESTAMP
2008-01-12 01:13:19 2008-01-12 01:13:19 2008-01-12 01:13:19
```
如果想得到不包括时间部分的当前日期，则可以使用CURDATE()函数，CURDATE()函数还有CURRENT_DATE等别名。如下：
```java  
SELECT CURDATE(),CURRENT_DATE
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
CURDATE() CURRENT_DATE
2008-01-12 2008-01-12
```
如果想得到不包括日期部分的当前时间，则可以使用CURTIME()函数，CURTIME()函数还有CURRENT_TIME等别名。如下：
```java  
SELECT CURTIME(),CURRENT_TIME
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
CURTIME() CURRENT_TIME
01:17:09 01:17:09
```
* MSQLServer
MSSQLServer中用于取得当前日期时间的函数为GETDATE()。如下：
```java  
SELECT GETDATE() as 当前日期时间
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
当前日期时间
2008-01-12 01:02:04.78
```
可以看到GETDATE()返回的信息是包括了日期、时间（精确到秒以后部分）的时间戳信息。MSSQLServer 没有专门提供取得当前日期、取得当前时间的函数，不过我们可以将GETDATE()的返回值进行处理，这里需要借助于Convert()函数。
使用CONVERT(VARCHAR(50) ,日期时间值, 101)可以得到日期时间值的日期部分，因此下面的SQL语句可以得到当前的日期值：
SELECT CONVERT(VARCHAR(50) ,GETDATE( ), 101) as 当前日期
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
当前日期
01/14/2008
```
使用CONVERT(VARCHAR(50),日期时间值,108)可以得到日期时间值的日期部分，因此下面的SQL语句可以得到当前的日期值：
```java  
SELECT CONVERT(VARCHAR(50) ,GETDATE(), 108) as 当前时间
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
当前时间
21:37:19
```
* Oracle
Oracle中没有提供取得当前日期时间的函数，不过我们可以到系统表DUAL 中查询SYSTIMESTAMP的值来得到当前的时间戳。如下：
```java  
SELECT SYSTIMESTAMP FROM DUAL
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
SYSTIMESTAMP
2008-1-14 21.46.42.78000000 8:0
```
同样，我们可以到系统表DUAL中查询SYSDATE 的值来得到当前日期时间。如下：
```java  
SELECT SYSDATE FROM DUAL
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
SYSDATE
2008-01-14 21:47:16.0
```
同样，Oracle中也没有专门提供取得当前日期、取得当前时间的函数，不过我们可以将SYSDATE的值进行处理，这里需要借助于TO_CHAR()函数，这个函数的详细介绍后面章节介绍，这里只介绍它在日期处理方面的应用。
使用 TO_CHAR(时间日期值, "YYYY-MM-DD") 可以得到日期时间值的日期部分，因此下面的SQL语句可以得到当前的日期值：
```java  
SELECT TO_CHAR(SYSDATE, "YYYY-MM-DD") FROM DUAL
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
TO_CHAR(SYSDATE,YYYY-MM-DD)
2008-01-14
```
使用TO_CHAR(时间日期值, "HH24:MI:SS") 可以得到日期时间值的时间部分，因此下面的SQL语句可以得到当前的日期值：
```java  
SELECT TO_CHAR(SYSDATE, "HH24:MI:SS") FROM DUAL
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
TO_CHAR(SYSDATE,HH24:MI:SS)
21:56:13
```
* DB2
DB2中同样没有提供取得当前日期时间的函数，不过我们可以到系统表SYSIBM.SYSDUMMY1中查询CURRENT TIMESTAMP的值来得到当前时间戳。如下：
```java  
SELECT CURRENT TIMESTAMP FROM SYSIBM.SYSDUMMY1
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
1
2008-01-14-21.58.20.01515000
```
从系统表SYSIBM.SYSDUMMY1中查询CURRENT DATE 的值来得到当前日期值。如下：
```java  
SELECT CURRENT DATE FROM SYSIBM.SYSDUMMY1
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
1
2008-01-14
```
从系统表SYSIBM.SYSDUMMY1中查询CURRENT TIME的值来得到当前日期值。如下：
```java  
SELECT CURRENT TIME FROM SYSIBM.SYSDUMMY1
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
1
22:05:48
```