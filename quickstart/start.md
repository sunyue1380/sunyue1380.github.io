# 快速入门

## 1 建立实体类
```java
//用户类
public class User {
    private long id;
    private String username;
    private String password;
}
```

> 实体类中必须有id属性.若有@Id注解则以@Id注解修饰的属性作为id属性,若无@Id注解则以变量名为id的属性作为id.

> id属性的类型必须为long型!

## 2 导入QuickDAO
QuickDAO基于JDBC,为提高效率,默认只支持数据库连接池.

* 导入commons-dbcp(或者其他的DataSource实现)
* 导入QuickDAO最新版本
```
<dependency>
   <groupId>commons-dbcp</groupId>
   <artifactId>commons-dbcp</artifactId>
   <version>1.4</version>
</dependency>
<dependency>
  <groupId>cn.schoolwow</groupId>
  <artifactId>QuickDAO</artifactId>
  <version>3.0</version>
</dependency>
```

## 3 使用QuickDAO
QuickDAO支持自动建表,自动新增字段功能.当您在Java代码中配置好QuickDAO后无需再对数据库做任何操作.

```java
BasicDataSource mysqlDataSource = new BasicDataSource();
mysqlDataSource.setDriverClassName("com.mysql.jdbc.Driver");
mysqlDataSource.setUrl("jdbc:mysql://127.0.0.1:3306/quickdao");
mysqlDataSource.setUsername("root");
mysqlDataSource.setPassword("123456");
//指定实体所在包名
cn.schoolwow.quickdao.dao.DAO dao = QuickDAO.newInstance()
                    .dataSource(mysqlDataSource)
                    .packageName("cn.schoolwow.quickdao.entity")
                    .build();
//之后所有的操作使用dao对象完成
```
