# dormitory_management_system_server
## 项目介绍
针对人群：对于刚学习完servlet、JDBC、Mysql的实战项目。
### 宿舍管理员管理
![image](https://github.com/user-attachments/assets/c246ec4b-dcb9-4cfb-9d39-f36715fcddaf)
#### 添加宿舍管理员
![image](https://github.com/user-attachments/assets/2d8fd736-bc26-4992-9c79-1ac0c7e7a6da)
### 学生管理
![image](https://github.com/user-attachments/assets/f349f712-e901-49da-ab2e-31448a919d0b)
#### 添加学生
![image](https://github.com/user-attachments/assets/c2ce0290-c82c-48d7-b4f7-3fcd7881b4c4)
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
## 技术选型
### 前端:html,css、jquery(is框架),bootstrap,Bootstrap中的datetimepicker插件
### 后端:jsp、servlet(接入层)、jdbc
### 数据库:mysql5.6
### 服务器:tomcat8.0
jsp的实质是servlet，而servlet是后端的技术，那么jsp应该属于后端
前端:用户能够直观看到的内容都是前端做的，包括HTML、CSS,JavaScript等
后端:用户不能直接看到的内容都是后端做的，jsp、Servlet(接入层)、jdbc等
## 项目分层
![image](https://github.com/user-attachments/assets/75bc9bdd-0e9e-4203-8b02-79cfc96f9a7a)
## 数据库设计
```
-- 用户表
CREATE TABLE `user`(
	`id` int NOT NULL AUTO_INCREMENT,
    	`name` varchar(20) NOT NULL,
    	`password` varchar(20) NOT NULL,
    	`stuCode` varchar(20) DEFAULT NULL COMMENT '学号',
	`dormCode` varchar(20) DEFAULT NULL COMMENT '宿舍编号',
    	`sex` varchar(10) DEFAULT NULL,
	`tel` varchar(15) DEFAULT NULL,
    	`dormBuildId` int DEFAULT NULL COMMENT '宿舍楼ID',
    	`role` int DEFAULT NULL COMMENT '超级管理员 0；宿舍管理员1；学生2',
    	`createUserId` int DEFAULT NULL COMMENT '创建人ID',
    	`disabled` int DEFAULT '0',
    	PRIMARY KEY (`id`),
    	UNIQUE KEY `stuCode` (`stuCode`),
    	KEY `dormBuildId` (`dormBuildId`),
    	KEY `createUserId` (`createUserId`),
    	CONSTRAINT `fk_createUserId` FOREIGN KEY (`createUserId`) REFERENCES `user` (`id`),
    	CONSTRAINT `fk_dormBuildId` FOREIGN KEY (`dormBuildId`) REFERENCES `dorm_build` (`id`)
);

-- 宿舍楼表
CREATE TABLE `dorm_build`(
	`id` int NOT NULL AUTO_INCREMENT,
    	`name` varchar(20) DEFAULT NULL,
    	`remark` varchar(255) DEFAULT NULL,
    	`disabled` int DEFAULT "0", 
    	PRIMARY KEY (`id`),
    	UNIQUE KEY `name` (`name`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4;
-- 一般都是逻辑删除，通过一个字段的值去判断该行数据是否已经被删除

-- 宿舍楼和宿舍管理员的中间表
-- 一个管理员可以管理多个宿舍楼，一个宿舍楼可以被多个人管理，多对多关系
CREATE TABLE `manage_dormbuild`(
	`id` int NOT NULL AUTO_INCREMENT,
    	`userId` int DEFAULT NULL,
    	`dormBuildId` int DEFAULT NULL,
    	PRIMARY KEY (`id`),
    	KEY `userId` (`userId`),
    	KEY `dormBuildId` (`dormBuildId`),
    	CONSTRAINT `userId` FOREIGN KEY (`userId`) REFERENCES `user` (`id`),
    	CONSTRAINT `dormBuildId` FOREIGN KEY (`dormBuildId`) REFERENCES `dorm_build` (`id`)
);
-- 缺勤表
CREATE TABLE `absence`(
	`id` int(11) NOT NULL AUTO_INCREMENT,
	`studentId` int(11) DEFAULT NULL COMMENT '学生id',
	`date` date DEFAULT NULL COMMENT '缺勤时间',
	`remark` varchar(50) DEFAULT NULL COMMENT '备注',
	`disabled` int(11) DEFAULT NULL,
	PRIMARY KEY (`id`),
	KEY `studentId` (`studentId`),
	CONSTRAINT `tb_record ibfk 1` FOREIGN KEY (`studentId`) REFERENCES `user` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8;
```sql
