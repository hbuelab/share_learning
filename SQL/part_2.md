2.1查询结果排序

order by 列名 asc,  列名 DESC

2.2 多个字段混合排序
order by 列名 列名 asc, 列名 desc

2.3
按照部分子串进行排序：其实是获取部分的字串：
substr(列名，length(列名) - 长度) （db2,or,mys,pg）

substring(列名，length(列名) - 长度) (ms ss)

2.4 对字母数字混合的数据排序

or和pg
使用函数replace和translate来修改
select data from v order by replace(data,replace(translate(data,'012','###'),'#',''),'')

db2
使用视图
ms ss 和mys暂不支持translate，无法解决

2.5 处理排序中出现的空值
db2,mys,pg,ss中用case表达式来标记一个值是否为NULL，在order by子句中增加标记列，就很容易控制空值是排在前面还是后面，
如：select name,comm from (select name,comm case when comm is null then 0 else 1 end as is_null from emp ) x order by is_null desc ,comm

or8以前可以用以上，or9以后在order by 语句后使用nulls first 或者null last来保证，就不用考虑空值的顺序了。


2.6 根据数据项的键排序

select ename ,sal,job,comm  from emp order by case when job = 'sales' then comm else sal end 