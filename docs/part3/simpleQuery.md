# 简单查询

DAO接口中定义了fetch方法,用于快速获取实体类信息.接口定义如下:

|名称|说明|
|---|---|
|<T> T fetch(Class<T> _class, long id);|根据id获取实体对象|
|<T> T fetch(Class<T> _class, String property, Object value);|根据指定属性获取对象(若返回结果有多个,则只返回第一行数据)|
|<T> List<T> fetchList(Class<T> _class, String property, Object value);|根据指定属性获取对象列表|

实例代码:
```java
//根据id查询
User user = dao.fetch(User.class,1);
//根据属性查询
User user = dao.fetch(User.class,"username","quickdao");
List<User> user = dao.fetchList(User.class,"password","123456");
```