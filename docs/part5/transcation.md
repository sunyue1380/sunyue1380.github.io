# 事务操作

DAO接口封装了简单的事务操作,以下是相关的API:

|名称|说明|
|---|---|
|void startTransaction();|开启事务|
|void rollback();|回滚|
|void commit();|提交事务|
|void endTransaction();|结束事务|
|Savepoint setSavePoint(String name);|设置保存点|
|void rollback(Savepoint savePoint);|回滚到保存点|

> 当您开启事务时,务必手动调用commit()方法提交事务.调用endTransaction()方法不会自动提交事务.

手动控制事务提交:

```
        dao.startTransaction();
        UserPlayList userPlayList = new UserPlayList();
        userPlayList.setUserId(1);
        userPlayList.setPlaylistId(2);
        logger.info("[插入用户播单订阅记录]实体:{},影响:{}",JSON.toJSONString(userPlayList),dao.save(userPlayList));
        //更新用户播单订阅数
        PlayList playList = dao.fetch(PlayList.class,1);
        playList.setSubscribeCount(playList.getSubscribeCount()+1);
        logger.info("[更新播单订阅数]实体:{},影响:{}",JSON.toJSONString(playList),dao.save(playList));
        dao.commit();
        dao.endTransaction();
        long count = dao.query(UserPlayList.class).addQuery("userId",1).count();
        logger.info("[检查用户播单订阅记录]count:{}",count);
        Assert.assertEquals(2,count);
```

开启事务插入一条订阅记录后回滚

```
        dao.startTransaction();
        userPlayList = new UserPlayList();
        userPlayList.setUserId(2);
        userPlayList.setPlaylistId(1);
        logger.info("[插入用户播单订阅记录]实体:{},影响:{}",JSON.toJSONString(userPlayList),dao.save(userPlayList));
        dao.rollback();
        dao.endTransaction();
        count = dao.query(UserPlayList.class).addQuery("userId",2).count();
        logger.info("[检查用户播单订阅记录]count:{}",count);
        Assert.assertEquals(0,count);
```