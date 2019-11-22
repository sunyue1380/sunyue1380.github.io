# 实体扫描

QuickDAO提供了自动建表功能,能够根据您配置的实体类包名扫描实体类并自动创建表.

## 样例

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
```

## 数据源

QuickDAO的所有操作全部基于DataSource,您需要传递给QuickDAO一个DataSource对象以便操作数据库.
您可以选择任何实现了DataSource接口的数据库连接池框架,例如dbcp,c3p0,druid等等.
例如导入dbcp, 您需要在pom.xml添加如下代码
```xml
<dependency>
    <groupId>commons-dbcp</groupId>
    <artifactId>commons-dbcp</artifactId>
    <version>1.4</version>
</dependency>
```

配置数据源

```java
BasicDataSource mysqlDataSource = new BasicDataSource();
mysqlDataSource.setDriverClassName("com.mysql.jdbc.Driver");
mysqlDataSource.setUrl("jdbc:mysql://127.0.0.1:3306/quickdao");
mysqlDataSource.setUsername("root");
mysqlDataSource.setPassword("123456");
QuickDAO.newInstance().dataSource(mysqlDataSource);
```

## 扫描实体类

QuickDAO提供了扫描实体类和过滤实体类的方法

* packageName("cn.schoolwow.quickdao.entity");

扫描包``cn.schoolwow.quickdao.entity``

* packageName("cn.schoolwow.quickdao.entity","t");

扫描包``cn.schoolwow.quickdao.entity``并为该包下所有的表添加前缀``t_``

* ignorePackageName("cn.schoolwow.quickdao.entity");

忽略包``cn.schoolwow.quickdao.entity``

* ignoreClass(User.class);

忽略User类

* filter(Predicate<Class> predicate);

自定义过滤方法

## 其他配置

* foreignKey(boolean openForeignKey)  

是否开启外键约束

* autoCreateTable(boolean autoCreateTable)  
 
是否自动建表

* autoCreateProperty(boolean autoCreateProperty)   

是否自动新增属性

