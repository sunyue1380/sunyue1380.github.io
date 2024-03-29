# 实体注解

QuickDAO提供了实体注解用于用户自定义字段属性.

## @Id

标识Id字段,作用于类字段上

```java
public class User{
    @Id
    private long uid;
}
```

## @ColumnNamne

映射字段名,作用于类字段上

```java
public class User{
    @ColumnName("uid")
    private long id;
}
```

## @TableName

映射表名,作用于类上

```java
@TableName("myUser")
public class User{
}
```

## @ColumnType

自定义数据库类型,作用于类字段上

```java
public class User{
    @ColumnName("varchar(1024)")
    private String username;
}
```

## @Comment

添加数据库注释,作用于类字段上

```java
public class User{
    @Comment("用户名")
    private String username;
}
```

## @Index

在该字段上建立索引,作用于类字段上

> 建议在有唯一性约束的字段上建立索引,以便加快检索速度

```java
public class User{
    @Index
    private String username;
}
```

## @Constraint

添加约束,包括是否非空,是否唯一,check约束以及默认值,作用于类字段上

* notNull 是否非空,默认为false
* unique 是否唯一,默认为false
* check check约束,默认为空
* defaultValue 默认值,默认为为空

```java
public class User{ 
    @Constraint(notNull=true, unique=true)
    private String username;
}
```

## @ForeignKey

添加外键约束,指定关联字段以及外键字段更新和删除时的策略,作用于类字段上

* table 关联到哪张表
* field 关联到表的哪个字段,默认为id
* foreignKeyOption 外键级联更新策略,默认为NOACTION

```java
public class User{ 
    @ForeignKey(table=Address.class,field="uid",foreignKeyOption=ForeignKeyOption.RESTRICT)
    private long addressId;
}
```

## @Ignore

忽略该类/忽略该字段,作用于类和类字段上

忽略age属性

```java
public class User{
    @Ignore
    private int age;
}
```

忽略Address类

```java
@Ignore
public class Address{
}
```

> QuickDAO会自动忽略实体类中集合类成员变量以及实体类成员变量

```java
public class User{
    private Address address;
    private List<Long> userIds;
    //以上属性均为自动被QuickDAO所忽略
}
```
