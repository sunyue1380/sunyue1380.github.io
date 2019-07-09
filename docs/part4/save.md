# 插入操作

QuickDAO提供了插入方法,定义在DAO接口中,其相关API如下:

|名称|说明|
|---|---|
|long save(Object instance);|保存实体对象|
|long save(Object[] instances);|保存实体列表|
|long save(List instanceList);|保存实体列表|

save方法的流程如下:
* save方法会先调用exist方法判断实体类是否已经存在在数据库中.
* 若已经在数据库中,则再判断实体类是否有唯一性约束,若有唯一性约束则根据唯一性更新,否则根据id更新.
* 若不存在,则执行插入操作.

实例代码如下:
```
        Comment newComment = new Comment();
        newComment.setAuthor("_前端农民工");
        newComment.setAvatar("https://r1.ykimg.com/0510000058CB4CA9429D3E61C9029307");
        newComment.setPublishTime(new Date());
        newComment.setContent("看到杨颖就想跳过");
        newComment.setVideoId(1);
        effect = dao.save(newComment);
```


