---
title: "集群信息"
description: test
draft: false
---

## 基本属性

这里显示了集群的基本信息。

![基本属性](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/basic_info.png)


## 服务端口信息

集群提供三个高可用 IP：

- 高可用读IP：可将请求在所有节点之间进行负载分担，提高读取性能，消除单点故障。

- 高可用写IP：始终指向 Master 节点。

- 高可用 Proxy IP：始终指向 Proxy 实例的 Master 节点。

![端口信息](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/port_info.png)

**注解**:

1. 务必使用读IP执行读请求，以将所有读请求按轮询方式分摊到所有节点；务必使用写 IP 执行写请求，以保证切主后不影响业务。
2. Proxy 实例用于读写分离。Proxy IP 作为集群预留 IP ，如未创建用 Proxy 实例该 IP 仍然被占用但是无法访问。

## 服务功能

点开基本属性旁边的下拉按钮，可以看到提供的服务功能。

![服务功能](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/service_list.png)

## 节点列表

显示了每个节点的服务状态。如果需要下载日志，需要点击标志，展示 IP 后进行下载。

![节点列表](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/node_list.png)

## 配置参数

这里列出了可以修改并持久化的配置参数。没有标注会重启服务的参数，都可以运行时修改，对服务没有影响。

![配置参数](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/env.png)

**注解**：会自动重启服务的参数已经在描述中说明，请在业务低峰时进行修改。

**部分参数说明**：

> 1. `Load_read_requests_to_master`，决定是否将读请求负载到 master 节点，默认为 `NO`，此时读请求只负载到 slave 节点。
> 2. `Audit_log_policy`，写审计日志的策略，提供 `ALL`、`LOGINS`、`QUERIES` 和 `NONE` 四种策略，默认为 `NONE`，此时不会记录审计日志。
> 3. `Audit_log_format`，审计日志文件格式，提供 `OLD`、`NEW` 和 `JSON` 三种格式，其中 `OLD` 和 `NEW` 分别为旧的和新的 XML 格式，注意修改该参数会自动重启服务。
> 4. `Audit_log_rotate_on_size`，单个审计日志文件大小，默认为 `100 MB`，范围为 `20 MB` ~ `2 GB`。
> 5. `Audit_log_rotations`，保留审计日志文件数量，默认为 `6`，支持最多保留 `48` 个文件。

## 监控告警

可以对集群节点配置告警策略，及时掌握集群的资源和服务状况。

![监控告警](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/alarm.png)

## 备份恢复

可以对集群进行手动备份，也可以在集群列表页面右键选择备份时间进行自动备份。

![手动备份](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/backup.png)
![自动备份](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/auto_backup.png)

如果需要从备份创建出一个独立于原有数据库服务的新数据库服务， 可以在详情页的『备份』标签下右键相应的备份点，再选择『从备份创建集群』即可。

![恢复集群](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/restore.png)

**注解**：仅备份主实例的主节点。恢复集群时会保留原集群的数据库账号密码。

###节点状态

展示主实例的角色信息。

![节点状态](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/display_nodeinfo.png)

**注解**：基础版集群不具备该功能。

## 账号列表

展示除运维账号外的 MySQL 账号。

![账号](C:/Original_qingcloud_doc/qingcloud-iaas-docs-master/database_cache/app_mysql_plus/_images/display_userlist.png)