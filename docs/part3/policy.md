# SQL���ɲ���

# ���������
QuickDAOʹ������ģʽ����SQL���:

```
select t.id as t_id,t.xx as t_xx, t1.id as t1_id,t1.xx as t1_xx,t2.id as t2_id,t2.xx as t2_xx from t join t1 on t.xx = t1.xx join t2 on t1.xx = t2.xx
```

QuickDAO��ά��һ��������,ÿ������joinTable����ʱ,�������ӱ�ı���.��һ��Ϊt1,�ڶ���Ϊt2,�Դ�����.