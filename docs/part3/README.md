# 查询

QuickDAO中的查询分为简单查询和复杂查询.简单查询是DAO接口中所定义的fetch方法,复杂查询是``dao.query(Class _class)``方法所返回Condition接口实例.

在本节中,需要区分两个概念:主表和子表.

# 主表

调用``dao.query(Class mainClass)``后mainClass实体类对应的表即为主表

# 子表

调用``dao.query(Class mainClass).joinTable(Class subClass)``,mainClass实体类对应的表为主表,subClass实体类对应的表为子表.