---
title: "修改健康检测配置"
descriptipn: 如何修改 NAT 网关的健康检测阈值。
draft: false
weight: 21
keyword: 云计算, NAT网关, NAT
---

NAT 网关支持自动进行健康检测，您可以根据实际需求修改需要检测的域名/地址及健康阈值。

## 检测原理

- NAT 网关节点健康检查：定时 ping NAT 网关的基础网络 IP，根据设置的健康检测阈值，判定 NAT 网关的线路健康状态。
- NAT 网关线路健康检查：定时 ping 设置的目标公网地址或者目标公网域名，根据设置的健康检测阈值，判定 NAT 网关的线路健康状态。

## 故障处理机制

- 一个 SNAT 规则可以绑多个公网 IP，并且设置健康检查，公网 IP 线路故障时，将自动切换流量，实现高可用。

- 根据公网 IP 的健康状态，将公网 IP 状态设置为 down 或者 up 并更新，处于 down 状态的公网 IP 所关联的 NAT 规则不会被下发。

## 默认配置

| 配置项        | 说明                                                     | 单位 | 默认值                                                   |
| ------------- | -------------------------------------------------------- | ---- | -------------------------------------------------------- |
| 健康阈值      | 连续检测结果为健康的次数，达到该值则认为是健康状态。     | 次   | 5                                                        |
| 不健康阈值    | 连续检测结果为不健康的次数，达到该值则认为是不健康状态。 | 次   | 5                                                        |
| 丢包率阈值    | 一次检测丢包率大于该值，则认为此次检测结果为不健康。     | %    | 30                                                       |
| 检查域名/地址 | 从 NAT 节点发 ping 包的目的地址。                        | -    | openapi.unionpay.com<br/>www.baidu.com<br>www.taobao.com |



## 操作步骤

1. 登录 管理控制台，在控制台导航栏中，选择**产品与服务** > **网络服务** > **NAT 网关**，进入 **NAT 网关**页面。

2. 在 NAT 网关列表中，目标 NAT 网关的 ID，进入详情页面。

3. 在基本信息区域，选择**更多操作** > **健康监测**，弹出**健康监测**配置窗口。

   <img src="../../../_images/health_check.png" />

4. 查看当前健康监测配置，根据实际需求，填写需要修改的阈值或域名地址。
5. 点击**确定**。
6. 修改成功后，需要点击**应用修改**使配置生效。

