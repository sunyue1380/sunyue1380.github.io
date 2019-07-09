# 部分查询

当您不需要返回一个实体类的所有字段信息时,您可以指定您需要返回的字段信息.

相关API如下:

|名称|说明|
|---|---|
|Condition addColumn(String field);|添加要返回的字段信息|
|List<T> getPartList();|获取部分字段返回结果|

通过getPartList方法返回的结果只会返回调用addColumn设置的那些字段信息.

以下是实例代码:

```
List<User> userList = dao.query(User.class)
                .addColumn("username")
                .addColumn("password")
                .getPartList();
```