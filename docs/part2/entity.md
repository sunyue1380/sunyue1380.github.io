# 实体类的扫描与过滤

## 扫描
QuickDAO允许您设定实体类所在包名,QuickDAO会扫描您所设定的包名并提取相关信息以供后面使用.
``QuickDAO.newInstance().packageName("cn.schoolwow.quickdao.entity)``

以上代码会扫描cn.scholwow.quickdao.entity这个包,并在数据库里自动生成对应表.数据库表名采用下划线命令,会将实体类的驼峰式命名转换.实体包下面可以继续建立包,生成的数据库表名会以@符号作为分隔.
例如这样一个实体类包
```
/User.java
/UserTalk.java
/user/User.java
/user/UserTalk.java
```
|类|表名|备注|
|---|---|---|
|User.java|user||
|UserTalk.java|user_talk|驼峰式改成下划线|
|/user/User.java|user@user|将文件夹和类名用@分隔|
|/user/UserTalk.java|user@user_talk|将文件夹和类名用@分隔|

## 别名

当需要扫描多个实体类包时,您可以设定别名.
``QuickDAO.newInstance().packageName("cn.schoolwow.quickdao.entity","t")``
以上代码在扫描实体包时,会在所有的数据库表名前添加``t_``前缀.

## 过滤
在某些情况下,您可能并不想扫描实体包下的某个类(它可能用于其他用途),此时您便可以调用过滤方法排除不需要建立数据库表的实体类.API方法如下:

|名称|说明|
|---|---|
|ignorePackageName|过滤包名|
|ignoreClass|过滤某个类|
|filter(Predicate<Class> predicate)|使用Predicate表达式过滤实体类|

当您调用以上API后,QuickDAO会忽略这些类,不会在数据库中生成对应的表