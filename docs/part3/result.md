# 返回结果

Condition接口对应有多种获取返回结果的方式,您需要根据您的查询条件调用不同的API以便获取相应的结果.获取返回结果的API分为几类.

> 分页操作返回结果默认为PageVo<T>对象.

## 获取总数

|名称|说明|
|---|---|
|long count();|获取总数|

根据查询条件获取总数

## 获取List

|名称|说明|
|---|---|
|T getOne();|根获取返回结果的第一行数据|
|List<T> getList();|获取实体列表|
|JSONArray getArray();|获取实体JSONArray数组|
|PageVo<T> getPagingList();|获取分页实体列表|

## 获取复杂对象

若主表中有复杂成员变量属性,则需要调用此类API才能填充主表复杂对象对应值.

|名称|说明|
|---|---|
|List<T> getCompositList();|获取实体类列表,填充其中的复杂类对象|
|JSONArray getCompositArray();|获取实体类JSONArray数组,填充其中的复杂类对象|
|PageVo<T> getCompositPagingList();|获取分页实体类列表,填充其中的复杂类对象|

> QuickDAO不会自动填充实体类复杂对象值,需要调用此类API才会自动填充.

## 获取单个属性列表

如果您需要某个表的id属性列表,您可以调用此API.

|名称|说明|
|---|---|
|<E> List<E> getValueList(Class<E> _class, String column);|获取单个属性列表|

例如调用``dao.query(User.class).getValueList(Long.class,"id")``会返回User表中的id属性列表``List<Long>``

## 获取部分属性列表

当您不需要返回表中所有字段信息时,您可以手动指定您需要返回的字段列.

|名称|说明|
|---|---|
|List<T> getPartList();|获取部分属性列表|
|PageVo<T> getPartPagingList();|获取分页部分属性列表|

## 获取聚合列表

您可以手动调用``addColumn``和``addAggerate``指定您要查询的聚合列和普通主表列.您必须调用``getAggerateList``才能获取对应的返回结果.

|名称|说明|
|---|---|
|JSONArray getAggerateList();|获取聚合查询返回列表|

> 以上各种返回结果您可以参考前面的章节查看它们的具体使用方法.