easystack、青云 云计算平台

openstack官方文档：docs.openstack.org

## 1.云计算

​	是一种**按量付费的模式**，是一个虚拟经集中管理平台，集群化管理**iass**，新增管理查看虚拟机

## 2.云计算的服务类型	

![Snipaste_2020-12-02_23-52-48](/Users/yutang/Documents/运维开发/asset/Snipaste_2020-12-02_23-52-48.png)

​	IAAS					 基础设施即服务 ECS云主机 自己部署环境，自己管理代码和数据
​								 Infrastructure as a Service
​	PASS docker	    平台即服务 提供软件的运行环境php，Java，python，go，c#，node js 自己管理代码和数据
​								 Platform as a Service
​	SAAS 				   软件即服务 企业邮箱，cdn，rds
​								 Software-as-a-Service

## 3.云计算IAAS功能

​	虚拟机的详细情况：硬件资源，ip统计情况
​	虚拟机管理平台：每台虚拟机的管理，都用数据库来统计	

## 4.openstack基于soa架构

​	传统的架构是mvc或者mvt，所有功能跑在一台服务器上，nginx服务关了所有功能都用不了

​	soa架构：拆业务，把每一个功能拆成独立的web服务，都拥有至少一个集群，千万用户同时访问

​	微服务框架：阿里的dubbo、Spring Boot

​	自动化代码上线：Jenkins + gitlab ci

​	自动化代码质量检查：sonarqube

​	目前流行的是Mitaka版，O版

## 5.虚拟机规划

​	