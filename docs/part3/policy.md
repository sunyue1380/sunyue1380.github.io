# SQL生成策略

# 表别名策略
QuickDAO使用以下模式生成SQL语句:

```
select t.id as t_id,t.xx as t_xx, t1.id as t1_id,t1.xx as t1_xx,t2.id as t2_id,t2.xx as t2_xx from t join t1 on t.xx = t1.xx join t2 on t1.xx = t2.xx
```

QuickDAO会维持一个计数器,每当调用joinTable方法时,会设置子表的别名.第一个为t1,第二个为t2,以此类推.