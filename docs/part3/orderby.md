# 排序与分页

QuickDAO支持排序分页操作,以下是相关API:

|名称|说明|
|---|---|
|Condition orderBy(String field);|按field升序排序|
|Condition orderByDesc(String field);|按field降序排序|
|Condition limit(long offset, long limit);|添加limit子句|
|Condition page(int pageNum,int pageSize);|分页操作|

其中orderBy和orderByDesc可多次调用.

以下是实例:

```
List<User> userList = dao.query(User.class)
   .page(1,10)
   .orderByDesc("id")
   .getList();
```