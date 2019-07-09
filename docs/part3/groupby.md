# 聚合查询

QuickDAO支持聚合查询,以下是相关API:

|名称|说明|
|---|---|
|Condition addAggerate(String aggerate,String field);|添加聚合查询,aggerate值可以为``COUNT,SUM,MAX,MIN,AVG``,默认别名为``aggerate(field)``,例如调用``addAggerate("COUNT","id")``别名为``COUNT(id)``|
|Condition addAggerate(String aggerate,String field,String alias);|添加聚合查询,aggerate值可以为``COUNT,SUM,MAX,MIN,AVG``,alias参数指定别名名称|
|Condition groupBy(String field);|添加group by子句|

添加聚合查询后,必须调用``getAggerateList()``获取聚合查询的结果,获取的结果为JSONArray格式.

当你添加了聚合查询后,你可以调用``addColumn(String field)``方法添加**主表**字段.

以下是实例:

```
JSONArray array = dao.query(PlayList.class)
                .addAggerate("SUM","subscribeCount")
                .addAggerate("COUNT","id","count(id)")
                .addColumn("tv")
                .groupBy("tv")
                .getAggerateList();
```
