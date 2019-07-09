# 条件克隆

Condition接口实现了Clone接口,这意味您可以克隆Condition对象.

某些情况下您可能会用到此方法,实例代码如下:

```
Condition condition = dao.query(User.class);
Condition cloneCondition = condition.clone();

condition.addQuery("type",1);
List<User> userList = condition.getList();

condition.addQuery("type",2);
List<User> userList = cloneCondition.getList();
```