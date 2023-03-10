# 隐喻
用概念去描述软件，方便理解
# 三思 21
![问题定义](问题的定义.png)
花在前期准备（问题定义、需求分析、软件架构）上的时间大概是20%~30%，工作量在10%~20%。
# 深入一种语言去编程
如果你使用的语言缺乏你希望用的构件，或者倾向于出现其他种类的问题，那就应该试着去弥补它。发明你自己的编码约定、标准、类库及其他改进措施。
# 设计是个了无章法的过程
设计永无止境，足够好的设计为：到你没时间再做了为止。
# 管理复杂度是软件开发中最重要的技术话题，软件的首要技术使命就是管理复杂度
## 管理复杂度的方法
- 在抽象的层次上工作，能减少人的脑力负担
- SOLID原则
- 把任何人在同一时间需要处理的本质(essential)复杂度减到最小；
- 不要让偶然(accidential)复杂度无谓地快速增长
## 设计的层次
![设计的层次](设计的层次.png)
④分解子程序：完整地定义出类内部的子程序，有助于更好地理解类的借口；反过来也有助于对类的接口的进一步修改（抽象）。
## 子系统（示例）
- service 业务规则系统
- ui 用户界面系统
- database 数据库系统（类拆解示例如下）
  1. 数据访问类(dao)
  2. 持久化框架(orm)
  3. 数据库元数据(entity)
- system 对系统的依赖性（可移植性）

