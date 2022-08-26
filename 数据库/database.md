# 数据库
## 一、创建视图
```sql
-- 获取今早凌晨的时间戳
select unix_timestamp(date_format(NOW(), '%Y-%m-%d'));
-- 1661097600
```
```sql
-- ioc.t_dws_indicator_compromise_0816 source
create VIEW ioc.t_dws_indicator_compromise_0822 AS
select * from ioc.t_dws_indicator_compromise where `timestamp` > 1661097600;
```
## 二、事务：每天自动创建视图
```sql
-- 获取今早凌晨的时间戳
select unix_timestamp(date_format(NOW(), '%Y-%m-%d'));
-- 1661097600
```
## 三、SQL 之中插入 计算
### 1. 与时间相关的函数
#### 参考：
<a href="https://blog.csdn.net/inflaRunAs/article/details/103594409" title="SQL时间戳">SQL 时间戳相关</a>
```sql
select now();
-- 2022-08-22 10:42:17 
select curdate();
-- 2022-08-22
select curtime();
-- 10:40:26 
```
### 2. 获取今早凌晨的时间戳
```sql
select unix_timestamp(date_format(NOW(), '%Y-%m-%d'));
-- 1661097600
```