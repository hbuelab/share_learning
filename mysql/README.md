# mysql笔记
## mysql自动管理时间戳
> mysql不支持默认值使用函数,并且只支持自动更新第一个字段时间戳,故第二个字段需要用触发器实现自动更新

create table time_test (
    ...
    `updated_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
    `created_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
);

> tips: timestamp 字段长度需为0

```mysql
DELIMITER $$
　　CREATE TRIGGER time_test_update
　　AFTER INSERT ON time_test FOR EACH ROW
    BEGIN
　　  SET NEW.created_time = NOW();
　　END;
$$
delimiter ;
```
