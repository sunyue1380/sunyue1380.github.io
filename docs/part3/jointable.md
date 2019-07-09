# 外键关联查询

QuickDAO支持复杂的外键关联查询,用户可以通过调用相关API实现强大的SQL外键查询功能.

> 本节会经常提及两个概念:主表和子表.

# Condition和SubCondition

调用``dao.query(PlayHistory.class)``会返回PlayHistory类的Condition接口对象.
在Condition接口对象上调用``joinTable(User.class, "user_id", "uid")``会返回SubCondition接口对象实例.
Condition类代表着对**主表**的操作,SubCondition代表着对**子表**的操作.

# API

外键关联相关API涉及Condition接口和SubCondition.相关API如下:

## Condition

|名称|说明|
|---|---|
|<T> SubCondition<T> joinTable(Class<T> _class, String primaryField, String joinTableField);|join子表,primaryField表示主表的关联字段,joinTableField表示子表的关联字段,即主表.primaryField = 子表.joinTableField|
|<T> SubCondition<T> joinTable(Class<T> _class, String primaryField, String joinTableField,String compositField);|同上一个方法相似,compositField参数表示主表中子表类型的字段名|

其中compositField参数显示指定主表中子表类型的字段名.若未指定,则默认获取主表中唯一一个类型为子表类型的成员变量. 您可以翻阅本节后面的**compositField**小节查看具体实例.

## SubCondition

子表可以继续关联子表,因此子表中也会有joinTable方法,它们功能同Condition类中的方法类似,只是从主表关联子表变成了子表关联子表.

当子表关联子表后,原子表我们称为该表的**父表**.例如以下代码:

```
Condition condition = dao.query(Report.class);
SubCondition subcondition = condition.joinTable(Talk.class, "talkId", "id");
SubCondition subcondition2 = subcondition.joinTable(User.class, "userId", "uid")
```
Report对应**主表**,Talk对应**子表**,同时也是User的**父表**,User对应**子表**.

以下是相关API:

|名称|说明|
|---|---|
|<T> SubCondition<T> joinTable(Class<T> _class, String primaryField, String joinTableField);|同Condition接口的功能类似|
|<T> SubCondition<T> joinTable(Class<T> _class, String primaryField, String joinTableField,String compositField);|同Condition接口的功能类似|
|SubCondition leftJoin();|使用左外连接|
|SubCondition rightJoin();|使用右外连接|
|SubCondition doneSubCondition();|返回子表的**父表**|
|Condition done();|返回主表|

SubCondition同样有复杂查询相关API和排序分页API,在此不再详细列出.

# compositField

``<T> SubCondition<T> joinTable(Class<T> _class, String primaryField, String joinTableField,String compositField);``接口中的compositField是指主表中的对应子表的成员变量.

```
//用户类
public class User {
    private long id;
    private String username;
    private String password;
//用户设置表
public class UserSetting {
    private long id;
    private long userId;
    private String setting;
    private User user;
```
调用``List<User> userList = dao.query(User.class).joinTable(UserSetting.class,"id","userId").getCompositList()`` 返回的UserSetting列表中,user属性不为空且为对应数据库记录.

> 若未显示指定compositField,则QuickDAO默认获取主表中类型为子表类型的成员变量.此时主表中对应子表成员变量只能有一个.

若主表中有多个子表对象,则必须显示指定compositField.

```
//用户类
public class User {
    private long id;
    private String username;
    private String password;
//用户关注表(userId关注followerId)
public class UserFollow {
    private long id;
    private long userId;
    private long followerId;
    private User user;
    private User followUser;
```

当关联查询时,需要显示指定对应的compositField.

```
List<UserSetting> userList = dao.query(UserFollow.class)
        //关联到User表的id字段,返回实体类信息放入变量名为user的实体类中
        .joinTable(User.class,"userId","id","user")
        .done()
        //关联到User表的id字段,返回实体类信息放入变量名为followUser的实体类中
        .joinTable(User.class,"userId","id","followUser")
        .done()
        //获取返回结果,UserFollow类中user和followUser都会返回信息
        .getCompositList();
```


# 实例代码

```
List<Report> reportList = dao.query(Report.class)
                .joinTable(User.class, "userId", "uid")
                .done()
                .joinTable(Talk.class, "talkId", "id")
                .joinTable(User.class, "userId", "uid")
                .joinTable(Project.class, "project", "key")
                .doneSubCondition()
                .done()
                .getList();
```