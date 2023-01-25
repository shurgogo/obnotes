```bash
\l # 查看所有数据库
\l 数据库名 # 查看某一数据库
\c 数据库名 # 以当前用户切换到数据库
\d # 查看所有表名
\d 表名 # 查看某一张表
drop user 用户名; # 删除用户
alter user 用户名 password '新密码'; # 修改密码
grant all privileges on table 表名 to 用户名; # 授予用户表所有权限
\q # 退出
create table 表名(
   ID INT PRIMARY KEY      NOT NULL, # 主键、非空
   SALARY         REAL     CHECK(SALARY > 0), # 检查必须大于0
   EMP_ID         INT      references COMPANY6(ID) # 外键
);
```