# tp5 model
db类方法:
查: find,select,value,column
增: insert,insertGetId,insertAll
改: update,setField,setInc
删: delete
模型方法:
查: get,find,all,select
增: data()->save,saveAll,create
改: save(data,where),saveAll,update       :isUpdate(true)
删: delete,destroy



## 查询
Db::table('think_user')->where('id',1)->find();
Db::table('think_user')->where('status',1)->select();

// 返回某个字段的值
Db::table('think_user')->where('id',1)->value('name');

// 返回数组
Db::table('think_user')->where('status',1)->column('name');
// 指定索引
Db::table('think_user')->where('status',1)->column('name','id');

# 添加
// 添加单条数据
db('user')->insert($data);
// 添加多条数据
db('user')->insertAll($list);