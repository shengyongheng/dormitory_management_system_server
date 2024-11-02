# dormitory_management_system_server
## 项目介绍
针对人群：对于刚学习完servlet、JDBC、Mysql的实战项目。
### 宿舍管理员管理
![image](https://github.com/user-attachments/assets/c246ec4b-dcb9-4cfb-9d39-f36715fcddaf)
### 学生管理
![image](https://github.com/user-attachments/assets/f349f712-e901-49da-ab2e-31448a919d0b)
### 宿舍楼管理
![image](https://github.com/user-attachments/assets/e83581ed-f661-4429-920a-20790762255b)
### 缺勤管理
![image](https://github.com/user-attachments/assets/77e6d359-1b51-4390-aefa-c421796009a2)
## 需求说明
1. 登录成功展示首页，将页面搭建起来(必须要先登录才可以进宿舍管理系统首页)。
  1.1 登录拦截器--2、3、4、5、7内的功能都需登录才可放行
  1.2 记住密码 cookie
2. 退出系统
3. 密码修改
4. 左侧宿舍管理员管理(只有超级管理员才能操作)
  4.1 增加
  4.2 删除、激活
  4.3 查:根据管理员的名字、性别、、电话号码、管理楼栋查询
5. 左侧学生管理(超级管理员可管理所有学生、宿舍管理员只能管理其管理楼栋的学生)
  5.1增加
  5.2删除、激活
  5.3修改
  5.4查:根据学生的名字、性别、电话号码、管理楼栋查询
6. 左侧宿舍楼管理(只有超级管理员才能操作)
  6.1增加
  6.2删除、激活
  6.3修改
  6.4查询
7. 缺勤管理
  7.1增加
  7.2删除、激活
  7.3修改
  7.4根据缺勤时间、学生楼栋、学生姓名或性别或宿舍编号查询
