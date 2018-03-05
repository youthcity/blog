# Mysql

## 索引

### 命名规则


### 常用命令

显示表的索引

```mysql
SHOW INDEX FROM tbl_a
```

创建索引

```mysql
CREATE INDEX idx_is_deleted_work_id_type ON tbl_a(is_deleted, work_id, type); 
```

删除索引
```mysql
 ALTER TABLE tbl_cloud_variable DROP INDEX idx_is_deleted_work_id_type;
```

## 创建大量数据

```mysql
DELIMITER $$
CREATE PROCEDURE prepare_data()
BEGIN
  DECLARE i INT DEFAULT 100;

  WHILE i < 100000 DO
    INSERT INTO your_table (val) VALUES (i);
    SET i = i + 1;
  END WHILE;
END$$
DELIMITER ;

# 然后调用程序
CALL prepare_data();
```

## mysql索引最左匹配原则的理解

[参考文章](https://www.zhihu.com/question/36996520)

## 增加、删除字段

```mysql
ALTER TABLE user ADD COLUMN `sex` varchar(255) NOT NULL DEFAULT '' AFTER `username`;
```

## 事务

## TRUNCATE TABLE 命令用于删除现有数据表中的所有数据

```mysql
TRUNCATE TABLE `tbl_user`; # 清空tbl_user内的数据
```

## 插入数据

### insert into

表示插入数据，数据库会检查主键，如果出现重复会报错； 

### replace into

表示插入替换数据，需求表中有PrimaryKey，或者unique索引，如果数据库已经存在数据，则用新数据替换，如果没有数据效果则和insert into一样； 

### insert ignore

如果表中如果已经存在相同的记录，则忽略当前新数据；

```mysql
# 创建表结构
CREATE TABLE tbl_test (
id INT NOT NULL PRIMARY KEY,
username VARCHAR ( 50 ),
age INT 
);

# 使用 insert into 添加数据，执行完后观察表内容
INSERT INTO tbl_test ( id, username, age )
VALUES
	( 1, 'bb', 13 );
 
 # 使用 insert ingnore 添加数据
INSERT IGNORE INTO tbl_test ( id, username, age )
VALUES
	( 1, 'aa', 13 );

# 使用 replace into 添加数据
REPLACE INTO tbl_test ( id, username, age )
VALUES
	( 1, "aa", 12 );
```
