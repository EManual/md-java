数据库就是数据的仓库，而DBMS是数据库的“管理员”。一些企业即生产食品又生产农用物资，这些产品都要保存到仓库中，同时企业内部也有一些办公用品需要保存到仓库中。
如果这些物品都保存到同一个仓库中的话会造成下面的问题：
l，不便于管理。食品的保存和复印纸的保存需要的保存条件是不同的，食品需要低温保鲜而复印纸则需要除湿，不同类的物品放在一起加大了管理的难度；
2，可能会造成货位冲突。食品要防止阳光直射造成的变质，因此要摆放到背阴面，同时为了防止受潮，也要把它们摆放到高处；办公用胶片也要避免阳光直射，所以同样要摆放到背阴面，而且胶片也要防潮，所以同样要把它们摆放到高处。这就造成两种货物占据的货位相冲突了。
3，会有安全问题。由于所有物品都放到一个仓库中没有进行隔离，所以来仓库领取办公用品的人员可能会顺手牵羊将食品偷偷带出仓库。
既然都是“仓库”，那么数据库系统也存在类似问题。如果企业将人力资源数据和核心
业务数据都保存到一个数据库中同样会造成下面的问题：
1，不便于管理。为了防止数据丢失，企业需要对数据进行定期备份，不过和核心业务数据比起来人力资源数据的重要性要稍差，所以人力资源数据只要一个月备份一次就可以了，而核心业务数据则需要每天都备份。如果将这两种数据保存在一个数据库中会给备份工作带来麻烦。
2，可能会造成命名冲突。比如人力资源数据中需要将保存员工数据的表命名为Persons，而核心业务数据也要将保存客户数据的表也命名为Persons，这就会相冲突了。
3，会有数据安全问题。由于所有的数据都保存在一个数据库中，这样人力资源系统的用户也可以访问核心业务系统中的数据，很容易造成数据安全问题。
显而易见，对于上边提到的多种物品保存在一个仓库中的问题，最好的解决策略就是使用多个仓库，食品保存在食品仓库中，农用物资保存在农用物资仓库中，而办公用品则保存在办公用品仓库中，这样就可以解决问题了。问了解决同样的问题，DBMS也采用了多数据库的方式来保存不同类别的数据，一个DBMS可以管理多个数据库，我们将人力资源数据保存在HR数据库中，而将核心业务数据保存在BIZ数据库中，我们将这些不同数据库叫做Catalog（在有的DBMS中也称为Database，即数据库）。采用多Catalog以后可以给我们带来如下好处：
1，便于对各个Catalog 进行个性化管理。DBMS 都允许我们指定将不同的Catalog保存在不同的磁盘上，由于人力资源数据相对次要一些，因此我们可以将HR保存在普通硬盘上，而将BIZ保存在RAID 硬盘上。我们还可以对每个Catalog所能占据的最大磁盘空间、日志大小甚至优先级进行指定，这样就可以针对不同的业务数据进行个性化定制了。
2，避免了命名冲突。同一个Catalog 中的表名是不允许重复的，而不同Catalog 中的表名则是可以重复的，这样HR 中可以有Persons 表，而BIZ 中也可以有Persons 表，二者结构可以完全不相同，保存的数据也不会互相干扰。
3，安全性更高。DBMS允许为不同的Catalog指定不同的用户，并且可以限定用户能访问的Catalog。比如用户hr123 只能访问HR，而用户sales001只能访问BIZ。这就大大加强了系统数据的安全性。