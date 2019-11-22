# 动态配置实体注解

QuickDAO提供了实体类扫描功能,实体扫描不仅能扫描本地实体包,也能够扫描第三方实体包.为了能够配置这些第三方实体包类的字段属性,提供动态配置实体注解的功能.

## 样例

```java
QuickDAO.newInstance()
                .packageName("cn.schoolwow.quickdao.entity")
                //定义User类
                .define(User.class)
                .tableName("user")
                //定义User类中的username字段
                .property("username")
                .notNull(true)
                .unique(true)
                .done()
                .done()
                .build();
```

> 调用define方法进行实体注解配置时,必须先配置要扫描的实体类包名.

## define方法

当配置好包名时,可以使用define方法指定实体类进行动态实体注解.

``define(User.class).tableName("t_user"')``

可以使用property方法配置字段属性

``define(User.class).property("username").notNull(true).unique(true).done();``
