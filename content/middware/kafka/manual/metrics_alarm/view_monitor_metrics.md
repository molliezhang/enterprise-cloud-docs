---
title: "查看资源和服务监控"
description: 本小节主要介绍 Kafka 主要支持哪些监控指标。 
keywords: Kafka 监控指标
weight: 40
collapsible: false
draft: false
---

Kafka 监控告警是通过 QingCloud 云监控告警服务为集群服务器的资源和服务提供监控管理。当集群监控项超过阈值时触发告警，并通过短信、邮件等形式发送告警通知。

QingCLoud 提供的云监控 CloudSat，可对 Kafka 的运行状态进行日常监控。您可以通过 CloudSat 管理控制台，一站式监控和告警 Kafka 各类服务、资源指标。

> 说明
> 
> 由于云监控 CloudSat 默认监控扫描周期为 5 分钟，则当前显示 5～10 分钟前的集群状态。

## 前提条件

- 已获取 QingCloud 管理控制台登录账号和密码，且已获取集群查看权限。
- 已创建 Kafka 集群，集群状态为**活跃**，且服务状态为**正常**。 
  
   > **说明**
   >
   > 更新中、异常、删除状态的集群，无法获取其监控指标。当集群重启或恢复后，即可正常查看。
  
- 集群服务已正常运行一段时间。
  
   > **说明**
   >
   > 监控扫描周期默认为 5 分钟，新增节点暂无法查看监控信息。

## 查看监控指标

1. 在集群管理页面，点击目标集群 ID，进入集群详情页面。
2. 在**节点**页签，选中目标节点**监控**。

   - 通过切换**服务**或**资源**，可分别查看对应节点服务和资源监控指标状态。
     > **注意**
     >
     > `客户端节点`不支持服务指标监控数据。
     
   - 通过切换时间区段，可分别查看不同时间段内集群性能状态。
     
     可选中`最近6小时`、`最近一天`、`最近两周`、`最近一个月`、`最近6个月`。
     
   - 您也可以通过自定义连续 7 天的起止时间，查看目标时间段内指标状态。
   
     但最多仅能查询近 90 天内数据。
   
   <img src="../../../_images/manual_node_monitor.png" alt="节点监控" style="zoom:50%;" />

## 查看实时监控

1. 在集群管理页面，点击目标集群 ID，进入集群详情页面。

2. 在**节点**页签，选中目标节点**监控**。

3. 查看实时服务指标状态。
   
   切换到**服务**指标，点击右侧状态按钮，将状态置为**开启**，开启实时监控。

   > **说明**
   >
   > 开启其中一个服务指标实时监控时，默认将开启全部服务指标实时监控。

   **实时监控为开启时**

   <img src="../../../_images/manual_service_monitor_realtime.png" style="zoom:50%;" />
   
4. 查看实时资源指标状态。

   切换到**资源**指标，点击右侧状态按钮，将状态置为**开启**，开启实时监控。

   > **说明**
   >
   > 每一个资源指标实时监控，需单独开启。

   **实时监控为开启时**

   <img src="../../../_images/manual_resource_monitor_realtime.png" style="zoom:50%;" />