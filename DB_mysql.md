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
