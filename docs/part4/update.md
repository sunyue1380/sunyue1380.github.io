# 更新操作

QuickDAO提供更新操作,可通过Condition接口类中的方法调用.其相关API如下:

|名称|说明|
|---|---|
|Condition addUpdate(String field, Object value);|添加要更新的字段信息|
|long update();|执行更新操作|

实例如下:

```
long count = dao.query(User.class)
                .addQuery("username","@")
                .addUpdate("password","123456")
                .update();
```