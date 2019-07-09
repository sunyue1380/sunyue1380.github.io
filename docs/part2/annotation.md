# 实体注解

QuickDAO允许您通过注解在实体类个性化实体类信息.目前支持的实体类注解如下:

|注解名|说明|示例|
|---|---|---|
|@ColumnType|自定义数据类型|@ColumnType("varchar(1024)"),字符型长度默认为255|
|@Comment|为字段或者表名添加注释|@Comment("用户id")|
|@DefaultValue|字段默认值|@DefaultValue("0")|
|@Id|标记主键字段|@Id|
|@Ignore|忽略该字段/忽略该类|@Ignore|
|@NotNull|是否非空|@NotNull|
|@Unique|是否唯一|@Unique|


# 外键注解
当启用外键约束时,必须要有@ForeignKey注解才能起效.
``@ForeignKey(table=User.class,field="id",foreignKeyOption=ForeignKeyOption.RESTRICT)
long userId``

以上代码用于表示userId字段为外键约束字段,它关联到User.class所对应的表的id字段,外键更新和删除时策略为``ForeignKeyOption.RESTRICT``.

外键策略有以下几种,默认为``ForeignKeyOption.RESTRICT``.

|约束|说明|
|---|---|
|ForeignKeyOption.RESTRICT|当在父表(即外键的来源表)中更新或删除对应记录时,首先检查该记录是否有对应外键，如果有则不允许更新或删除。|
|ForeignKeyOption.NOACTION|意思同restrict.即如果存在从数据，不允许更新或删除主数据|
|ForeignKeyOption.SETNULL|当在父表(即外键的来源表)中更新或删除对应记录时，首先检查该记录是否有对应外键，如果有则也更新或删除外键在子表（即包含外键的表）中的记录|
|ForeignKeyOption.CASCADE|当在父表(即外键的来源表)中更新或删除对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为null(不过这就要求该外键允许取null)|

