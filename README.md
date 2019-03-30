
# 分布式事务--基于可靠消息的最终一致性解决方案demo

![Spring Boot 2.0](https://img.shields.io/badge/Spring%20Boot-2.0-brightgreen.svg)
![Mysql 5.6](https://img.shields.io/badge/Mysql-5.6-blue.svg)
![JDK 1.8](https://img.shields.io/badge/JDK-1.8-brightgreen.svg)
![Maven](https://img.shields.io/badge/Maven-3.3.9-yellowgreen.svg)


## 项目使用技术

springboot、dubbo、zookeeper、activeMQ、定时任务

## 一、项目结构

maven父子工程：

父工程：consis

子工程：api-service、order、product、message

api-service:该项目主要是提供接口调用的，还包含实体类、枚举等一些通用内容

order:该项目是专门处理订单相关操作的系统

product:该项目是专门处理产品相关操作的系统

message:该项目是提供消息服务的系统，好包括定时任务


它们的依赖关系如下图：

![enter image description here](https://images.gitbook.cn/a181d460-acf7-11e8-afe5-6ba901a27e1b)

## 二、启动项目

首先在不同的系统中建立自己对应的数据库，springdatajpa会自动帮你生成表

注意启动顺序，如下：

* 启动zookeeper
* 启动activemq
* 启动tomcat，访问dubbo-admin管理控制台
* 启动MessageApplication
* 启动ProductApplication
* 启动OrderApplication

启动成功后，就可以通过postman工具进行测试
http://localhost:8082/createOrder
{
	"buyerId": 10029122,
	"list": [{
			"id": "101",
			"num": 2,
			"product": {
				"id": 101,
				"productName": "苹果手机保护套",
				"productPrice": 125,
				"productSku": 524,
				"productSpec": "保护套",
				"createTime": "2018-03-11 12:00:00",
				"remark": "高大上的保护套"
			}
		},
		{
			"id": "102",
			"num": 2,
			"product": {
				"id": 102,
				"productName": "苹果手机XR MAX",
				"productPrice": 8888,
				"productSku": 123,
				"productSpec": "苹果顶配手机",
				"createTime": "2018-03-11 12:00:00",
				"remark": "高大上的手机"
			}
		}
	]
}

