1. 用 brew 安装 postgresql
```bash
brew install postgresql
```
2. 安装完后查看版本
```bash
psql --version
```
3. 初始化, 如果不行则用 sudo
```bash
initdb /usr/local/var/postgres
```
4. 设置开机自启动（可选，未测试）
```bash
ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
```
5. 手动启动
```bash
pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start
```
6. 数据库初始化
```bash
psql postgres # 进入postgres数据库，默认用户为主机用户
create user 用户名 with password; '密码' # 创建root用户
create database 数据库名;
grant all privileges on database 数据库名 to 用户名; 
```
7. 手动停止
```bash
pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log stop -s -m fast
```
8. 其他 pg 命令行工具
```bash
createuser 用户名 -P 密码 # 生成用户
createdb 数据库名 -O 用户名 -E UTF8 -e # 生成属于某用户的数据库
```

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
