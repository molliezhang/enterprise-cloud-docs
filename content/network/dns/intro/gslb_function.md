---
title: "GSLB 功能特性"
date: 2021-04-28T00:38:25+09:00
description: 云解析服务 功能简介
weight: 20
draft: false
enableToc: false
keyword: GSLB 功能简介
---


## 功能简介

- 地址池配置

   地址池是 GSLB 管理的应用服务地址（IP 或域名）集合。一组地址池即相同区域的 IP 或域名地址，为一组应用提供服务。
   一个 GSLB 实例可以配置多组地址池，可实现不同地区的用户根据就近原则访问不同的地址池，同时可实现地址池容灾备份切换。

- 调度策略

  调度策略即通过设定流量调度策略，为不同网络或区域来源的访问用户设置不同的解析响应地址池，并实现用户就近访问和故障切换，帮助企业轻松管理全球流量。

  GSLB 支持基于访问延时的调度策略，即通过探测用户访问延时情况，将终端用户的请求路由到延迟最低的应用服务器集群上，实时切换到可用 IP，保障业务稳定运行。

- 健康监控

   健康监控针对 GSLB 地址池里 IP 地址，实时监测应用服务的可用性状态，支持 TCP 监控和 HTTP(S)监控。

- 故障切换

   当主地址池整体不可用时，GSLB 故障跌宕功能自动将用户访问流量切换到备地址，确保应用服务能无间隙响应用户的 DNS 查询请求，降低业务中断的风险，保障业务的稳定运行。