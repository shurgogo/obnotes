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

