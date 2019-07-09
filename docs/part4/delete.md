# 删除操作

Quick提供删除操作,在DAO接口和Condition接口都有提供相应API.

# DAO

DAO接口中的相关API如下:

|名称|说明|
|---|---|
|long delete(Class _class, long id);|根据id删除记录|
|long delete(Class _class, String field, Object value);|根据指定字段属性删除记录|
|long clear(Class _class);|清空表|

实例代码如下:

```
dao.delete(User.class,1);
dao.delete(User.class,"username","quickdao@schoolwow.cn");
dao.clear(User.class);
```

# Condition

Condition接口中相关API如下:

|名称|说明|
|---|---|
|long delete();|根据查询条件删除记录|

实例代码如下:

```
long count = dao.query(User.class)
                .addQuery("username","quickdao")
                .delete();
```