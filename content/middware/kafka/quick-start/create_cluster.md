---
title: "步骤一：创建 Kafka 集群"
date: 2021-11-15T00:40:25+09:00
description: 
weight: 10
draft: false
---

本小节主要介绍如何通过管理控制台快速创建 Kafka 集群。

## 前提条件

- 已获取管理控制台登录账号和密码，且账号已实名认证。
- 已获取 Kafka 集群操作权限。
- 在创建 Kafka 集群前，建议先创建好网络资源和依赖的服务资源：
  + 先创建一个 VPC 网络，再创建一个受管私有网络并加入 VPC 中，并开启 DHCP 服务（默认开启）。
      > **说明**
      >
      > 为了保障数据安全，Kafka 集群需要运行在受管私有网络中。
  + 在 QingCloud AppCenter 中创建一个 Zookeeper 集群，且 Kafka 与 ZooKeeper 需要在同一个 VPC 中。
      > **说明**
      >
      > 其他地方创建的 ZooKeeper 集群可能无法识别。

## 创建 Kafka 集群

1. 登录管理控制台。
2. 选择**产品与服务** > **消息队列与中间件** > **Kafka服务**，进入 Kafka 集群管理页面。
3. 点击**立即部署**或**创建**，进入应用部署页面。
4. 选择**区域**。
   根据就近原则，选择实例所在区域。
5. 配置实例基本信息、应用版本、网络信息、环境参数等信息。

   a. [基本设置](#第一步基本设置)

   b. [Kafka 节点设置](#第二步kafka-节点设置)

   c. [客户端节点设置](#第三步客户端节点设置)

   d. [网络设置](#第四步网络设置)

   e. [依赖服务设置](#第五步依赖服务设置)

   f. [服务环境参数设置](#第六步服务环境参数设置)

   g. [用户协议](#第七步用户协议)

6. 确认配置和费用信息无误后，点击**提交**，创建集群。

   集群创建成功后，可在**集群管理**页面，查看和管理 Kafka 集群。

   ![集群列表](../../_images/kafka_cluster_list.png)

### 第一步：基本设置

集群名称、版本、计费方式、部署方式等基本信息配置。

|<span style="display:inline-block;width:140px">参数</span> |<span style="display:inline-block;width:520px">参数说明</span>|
|:----|:----|
|   UUID     |  系统默认分配的全局唯一标识码，不可修改。  |
|   名称     |  输入当前集群的名称。 默认为`Kafka`。  |
|   描述  |  （可选）对集群的简要描述。   |
|   版本 |  选择集群版本，建议选择最新版本。|
|   计费方式 |  选择集群计费方式，可选择按**小时**、**月**、**年**计费。|
|   部署方式 |  <span style="display: block; background-color: #D8ECDE; padding: 10px 24px; margin: 10px 0; border-left: 3px solid #00a971;"><b>说明</b>: 仅**北京3区**区域支持选择部署方式。<li> **多可用区部署**：集群所有节点分散部署在当前 region 中的所有 zone，可用性高。</li><li> **单可用部署**：集群所有节点部署在当前region中的某一个zone 中，网络延迟最低。</li></span> |

![](../../_images/base_setup.png)

### 第二步：Kafka 节点设置

CPU、内存、节点数量、节点类型和存储容量根据自己实际需求进行选择即可。

|<span style="display:inline-block;width:140px">参数</span> |<span style="display:inline-block;width:520px">参数说明</span>|
|:----|:----|
|   CPU     |  选择 Kafka 节点云服务器 CPU 规格。  |
|   内存     |  选择 Kafka 节点云服务器内存大小。  |
|   节点数量  |  选择 Kafka 节点云服务器数量，至少 3 个节点。  |
|   节点类型  |  选择 Kafka 节点类型。支持  `基础型`和`企业型 e2` 和`企业型 e3`。|
|   存储容量 |  配置 Kafka 节点的磁盘大小。请根据业务量进行设置，可滑动设置或输入数字配置集群磁盘大小。| 

![](../../_images/kafka_node.png)

### 第三步：客户端节点设置

建议配置 Client 节点，否则某些功能无法使用（除非手动下载相关软件包并配置好）。

> **说明**
> 
> + Kafka 2.3.1 -QingCloud 2.0.1（包含）之前版本：客户端节点用户名为 ubuntu，初始密码为 kafka。
> + Kafka 2.3.1 -QingCloud 2.0.1之后版本：客户端节点用户名为 client，初始密码为 client。

|<span style="display:inline-block;width:140px">参数</span> |<span style="display:inline-block;width:520px">参数说明</span>|
|:----|:----|
|   CPU     |  选择客户端节点云服务器 CPU 规格。  |
|   内存     |  选择客户端节点云服务器内存大小。  |
|   节点数量  |  选择客户端节点云服务器数量。  |
|   节点类型  |  选择客户端节点类型。支持  `基础型`、`企业型 e2` 和`企业型 e3`。|
|   存储容量 |  配置客户端节点的磁盘大小。请根据业务量进行设置，可滑动设置或输入数字配置集群磁盘大小。| 

![](../../_images/client_node.png)

### 第四步：网络设置

为了保障数据安全，所有的集群都需要部署在受管私有网络中，请选择您创建的网络。

|<span style="display:inline-block;width:140px">参数</span> |<span style="display:inline-block;width:520px">参数说明</span>|
|:----|:----|
|   VPC网络     |  选择 VPC 网络。<li>默认适配同区域已有的 VPC 网络。可在下拉框选择已有 VPC 网络。<li>若无可选 VPC 网络，可点击**新建VPC网络**，创建依赖网络资源。  |
|   私有网络     |  选择私有网络。<li>默认适配同区域已有的私有网络。可在下拉框选择已有私有网络。<li>若无可选私有网络，可点击**新建私有网络**，创建依赖网络资源。  |
|   节点 IP   |  配置节点 IP 地址。<li>默认为`自动分配`。<li> 选择`手动配置`需为各节点配置 IP。  |

![](../../_images/network_setup.png)

### 第五步：依赖服务设置

选择您所依赖的 ZooKeeper 集群。
> **说明**
> 
> 若无可选资源，可点击**快捷创建**创建一个 ZooKeeper 集群。

![](../../_images/dependence_service.png)

### 第六步：服务环境参数设置

按照实际需求配置 Kafka 参数，同时也可以配置Kafka-manager是否需要登录，登录帐号与密码和端口参数。

> **注意**
> 
> offsets.topic.replication.factor 参数必须小于或者等于 Kafka broker 节点数，否则不能消费消息。

集群创建成功后，可在集群详情页面**配置参数**页签对参数进行修改。

![](../../_images/sevice_parameter.png)

### 第七步：用户协议

阅读**云平台 AppCenter 用户协议**，并勾选用户协议。

![用户协议](../../_images/user_agreement.png)


## 配置告警通知

集群创建完成后，请配置告警通知，以便及时了解集群资源的使用情况和集群服务的各项监控指标，当集群、节点、服务有异常时，可以及时获取异常信息。

详细操作请参见[设置监控告警](../../manual/metrics_alarm/set_alarm_rules/)。