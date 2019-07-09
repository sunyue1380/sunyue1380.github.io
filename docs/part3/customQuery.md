# 自定义查询

QuickDAO支持JSON格式的自定义查询条件.相关API如下:

|名称|说明|
|---|---|
|Condition addJSONObjectQuery(JSONObject queryCondition);|添加自定义JSON查询条件|

JSON格式化如下:
```
{
  {field}:{value},//字段查询
  {field}Start:{value},//添加大于等于查询
  {field}End:{value},//添加小于等于查询
  {field}IN:[array],//添加IN查询
  {field}NOTNULL:{value},//添加not null查询
  {field}NULL:{value},//添加null查询
  _orderBy:{value},//升序排列
  _orderByDesc:{value},//降序排列
  _pageNumber:{value},//页码
  _pageSize:{value},//每页个数
  //关联查询部分
  _joinTables:[
      {
         _class:{className} //关联类,例如<b>top.cqscrb.courage.entity.User</b>
         _primaryField:{primaryField} //主表关联字段
         _joinTableField:{joinTableField} //子表关联字段
         {field}:{value},//字段查询
         {field}Start:{value},//添加大于等于查询
         {field}End:{value},//添加小于等于查询
         {field}IN:[array],//添加IN查询
         {field}NOTNULL:{value},//添加not null查询
         {field}NULL:{value},//添加null查询
         _orderBy:{value},//升序排列
         _orderByDesc:{value},//降序排列
         _joinTables:[...] 更多关联查询
      }
  ]
}
```

实例如下:
```
String s = {
	"_joinTables": [{
		"uid":2,
		"_class": "cn.schoolwow.quickdao.entity.user.User",
		"_primaryField": "userId",
		"_joinTableField": "uid"
	},
	{
		"_class": "cn.schoolwow.quickdao.entity.user.Talk",
		"_primaryField": "talkId",
		"_joinTableField": "id",
		"_joinTables": [{
			"username":"sunyue@schoolwow.cn",
			"_class": "cn.schoolwow.quickdao.entity.user.User",
			"_primaryField": "userId",
			"_joinTableField": "uid",
			"_joinTables": [{
				"_class": "cn.schoolwow.quickdao.entity.logic.Project",
				"_primaryField": "project",
				"_joinTableField": "key"
			}]
		}]
	}]
}
JSONObject queryCondition = JSON.parse(s);
List<Report> reportList = dao.query(Report.class).addJSONObjectQuery(queryCondition).getList();
```