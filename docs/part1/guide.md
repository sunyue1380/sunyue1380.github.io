# 快速入门

此章节将引导您将QuickDAO用于您的项目中.在您配置过程所涉及到的API您可以翻阅后面的章节获取更多信息.

# 1 引入QuickDAO

QuickDAO为了提高效率,默认只支持数据库连接池.

# 1.1 导入commons-dbcp(或者其他的DataSource实现)
```
<dependency>
   <groupId>commons-dbcp</groupId>
   <artifactId>commons-dbcp</artifactId>
   <version>1.4</version>
</dependency>
```

# 1.2 导入QuickDAO
```
<dependency>
  <groupId>cn.schoolwow</groupId>
  <artifactId>QuickDAO</artifactId>
  <version>2.7</version>
</dependency>
```

您也可以[点此下载](https://oss.sonatype.org/service/local/artifact/maven/redirect?r=releases&g=cn.schoolwow&a=QuickDAO&v=2.7&e=jar)QuickDAO的jar包.

# 2 初始化QuickDAO

> 实体类中必须有Id属性,且类型只能为long型.QuickDAO默认将实体类中成员变量为id的属性作为id属性.若有@Id注解,则将@Id注解的属性作为id属性.

在使用QuickDAO之前,您需要先初始化.初始化代码如下:
```
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

首先配置数据库连接池,设置驱动类,用户名和密码,然后配置QuickDAO的数据库源和需要扫描的实体类包名,最后调用``build()``方法返回DAO接口实例.之后的所有操作都是通过这个dao对象完成的.至此,初始化完成.