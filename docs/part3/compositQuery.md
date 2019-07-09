# 复杂查询

Condition接口封装了数据库查询相关的API,您可以通过``dao.query(Class _class)``返回的Condition接口实例来添加查询操作.这些查询操作全部遵循链式操作,因此您可以一直点点点下去.

以下是查询相关API:

|名称|说明|
|---|---|
|Condition distinct();|添加distinct语句|
|Condition addNullQuery(String field);|field为null|
|Condition addNotNullQuery(String field);|field不为null|
|Condition addNotEmptyQuery(String field);|field不为null也不会空字符串|
|Condition addInQuery(String field, Object[] values);|添加IN查询条件|
|Condition addInQuery(String field, List values);|添加IN查询条件|
|Condition addNotInQuery(String field, Object[] values);|添加NOT IN查询条件|
|Condition addNotInQuery(String field, List values);|添加NOT IN查询条件|
|Condition addBetweenQuery(String field, Object start,Object end);|添加Between语句|
|Condition addQuery(String query);|添加自定义查询语句,**使用此API前请您先阅读[SQL生成策略](part3/policy.md)**|
|Condition addQuery(String field, Object value);|field=value|
|Condition addQuery(String field, String operator, Object value);|operator为操作符,值为``=,!=,>,>=,<,<=``中的一种|

以下是实例代码:
```
Condition<User> userCondition = dao.query(User.class)
                .distinct()
                .addQuery("username","@")
                .addQuery("type",">=",1)
                .addInQuery("token",new String[]{"7a746f17a9bf4903b09b617135152c71","9204d99472c04ce7abf1bcb9773b0d49"})
                .addNotNullQuery("lastLogin");
List<User> userList = userCondition.getList();
```