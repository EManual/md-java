前面演示的例子都是检索出表中所有的数据，不过在很多情况下我们需要按照一定的过滤条件来检索表中的部分数据，这个时候可以先检索出表中所有的数据，然后检查每一行看是否符合指定的过滤条件。比如我们要检索出所有工资少于5000元的员工的姓名，那么可以编写下面的代码来处理：
```java  
result = executeQuery(“SELECT FName, FSalary FROM T_Employee”);
for(i=0;i<result.count;i++)
{
	salary = result[i].get(“FSalary”);
	if(salary<5000)
	{
		name = result[i].get(“FName”);
		print(name+”的工资少于5000 元，为:”+salary);
	}
}
```
这种处理方式非常清晰简单，在处理小数据量以及简单的过滤条件的时候没有什么不妥的地方，但是如果数据表中有大量的数据（数以万计甚至百万、千万数量级）或者过滤条件
非常复杂的话就会带来很多问题：
1，由于将表中所有的数据都从数据库中检索出来，所以会有非常大的内存消耗以及网络资源消耗。
2，需要逐条检索每条数据是否符合过滤条件，所以检索速度非常慢，当数据量大的时候这种速度是让人无法忍受的。
3，无法实现复杂的过滤条件。如果要实现“检索工资小于5000或者年龄介于23岁与28岁之间的员工姓名”这样的逻辑的话就要编写复杂的判断语句，而如果要关联其他表进行查询的话则会更加复杂。
数据检索是数据库系统的一个非常重要的任务，它内置了对按条件过滤数据的支持，只要为SELECT 语句指定WHERE 语句即可，其语法与上一章中讲的数据更新、数据删除的WHERE语句非常类似，比如完成“检索出所有工资少于5000 元的员工的姓名”这样的功能可以使用下面的SQL语句：
```java  
SELECT FName FROM T_Employee WHERE FSalary<5000
```
执行完毕我们就能在输出结果中看到下面的执行结果：
```java  
FName
Jerry
Jane
Smith
Stone
```
WHERE子句还支持复杂的过滤条件，下面的SQL语句用来检索出所有工资少于5000元或者年龄大于25岁的员工的所有信息：
```java  
SELECT * FROM T_Employee WHERE FSalary<5000 OR FAge>25
```
执行完毕我们就能在输出结果中看到下面的执行结果：
  
使用WHERE子句只需指定过滤条件就可以，我们无需关心数据库系统是如果进行查找的，数据库会采用适当的优化算法进行查询，大大降低了CPU资源的占用。