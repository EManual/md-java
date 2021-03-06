员工表中的每一行记录代表了一个员工，一般员工的名字就能唯一标识这一个员工，但
是名字也是有可能重复的，这时我们就要为每一名员工分配一个唯一的工号：
  
这样就可以通过这个工号来唯一标识一名员工了。当老板下令说“把王二小提升为副总”的时候，我们就要问“公司有两个王二小，您要提升哪一个？”，老板可以说“技术支持部的王二小”，但是更好的方式，那就是说“提升工号为的002 员工为副总”，因为只有002这个工号才能唯一标识一名员工。这里的“工号”被称为员工表的“主键”（PrimaryKey），
所以我们可以说能唯一标识一行记录的字段就是此表的主键。
有的公司比较懒惰，不想为员工分配工号，只是硬性规定：一个部门中员工的姓名不能重复，有姓名重复的必须调换到其它部门。这样“部门”和“姓名”这两个字段加在一起就能唯一标识一名员工了，这里的“部门”和“姓名”两个字段就被称为“复合主键”，也就是任何一个字段都不能唯一标识一行数据，只有构成“复合主键”的所有字段组合起来才能
唯一标识这一行数据。
在大多数DBMS 中并没有强制规定一个表必须有主键，也就是一个表可以没有主键，但是为一个数据表指定一个主键是一个非常好的习惯。在后边的章节我们将提到用一个无意义的字段做主键将会更加有利于系统的可扩展性。