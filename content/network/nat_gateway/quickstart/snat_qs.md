---
title: "通过 SNAT 功能实现访问公网服务"
descriptipn: 通过 NAT 网关的 SNAT 功能云服务器访问公网。
draft: false
weight: 10
keyword: 云计算, NAT网关, NAT, SNAT, DNAT
---

您可以使用 NAT 网关的 SNAT 功能，为 VPC 中无公网 IP 的云服务器提供访问互联网的代理服务。

## 前提条件

- 已创建 VPC 网络。具体操作，请参见[创建 VPC 网络](/network/vpc/manual/vpcnet/10_create_vpc/)。


- 如果要创建以私有网络为粒度的 SNAT 规则，请确保 NAT 网关所属 VPC 中已经创建了私有网络。具体操作，请参见[连接私有网络](/network/vpc/manual/vpcnet/15_bind_vxnet/)。
- 如果要创建以云服务器为粒度的 SNAT 规则，请确保 NAT 网关所属 VPC 中已经创建了云服务器。具体操作，请参见[创建云服务器](/compute/vm/quickstart/create_vm/)。

## 配置流程

![](../../_images/snat_qs.svg)

## 操作步骤

### 步骤1：创建 NAT 网关

1. 登录 管理控制台，在控制台导航栏中，选择**产品与服务** > **网络服务** > **NAT 网关**，进入 **NAT 网关**页面。

2. 点击**创建**，进入**创建 NAT 网关**页面。

   ![](../../_images/create_natgw.png)

3. 配置 NAT 网关信息。

   对于 NAT 网关的各项配置参数更详细的说明，可参见[创建 NAT 网关](../../manual/mge_nat/create_nat/)。

   - **区域**：选择需要创建 NAT 网关的区域。
   - **名称**：设置 NAT 网关的名称。名称长度为1~64个字符，须由中文、英文字母、数字、下划线（_）、中划线（-）和点（.）组成。
   - **VPC 网络**：选择 NAT 网关所属的 VPC。创建 NAT 网关后，不能修改 NAT 网关所属的 VPC。
   - **规格**：选择 NAT 网关的规格。不同规格的 NAT 网关会影响 SNAT 最大连接数和 流量转发能力，但不会影响 DNAT 性能。请您根据业务需求灵活选择规格。规格说明请参考 [NAT 网关规格](../../intro/specification/)。
   - **部署方式**：选择 NAT 网关集群节点部署方式。**多可用区部署**表示节点分散部署在不同可用区，可用性更高；**单可用区部署**表示节点部署在指定的同一可用区，网络延迟最低。
   - **可用区**：选择**单可用区部署**方式时，需要指定 NAT 网关所属的可用区。
   - **公网 IP**：NAT 网关需要绑定 EIP 才能正常工作。推荐选择**购买并绑定**。
   - **安全组**：选择 NAT 网关的安全组。
   - **集群模式**：选择**多可用区部署**方式时，需要选择 NAT 网关节点的集群模式。**低延时**表示网络流量会优先传输到距离最近的 NAT 网关节点上；**单高吞吐**表示网络流量会均衡地传输到所有的 NAT 网关节点上。

4. 点击**立即创建**。等待创建完成。

### 步骤2：配置指向 NAT 网关的路由

>**注意**
>
>- 若 NAT 网关所属的 VPC 是您在新版 NAT（ NATGW v2.0） 上线之后新建的，则系统会在创建 NAT 网关时自动在该 VPC 的默认路由表中下发指向 NAT 网关、目标网络为 0.0.0.0/0 的路由，无需您手动进行配置，请跳过本步骤，直接执行[步骤3](#步骤3添加-snat-规则)。
>- 若 NAT 网关所属的 VPC 是您在新版 NAT（ NATGW v2.0） 上线之前创建的，或者该 VPC 关联的默认路由表中已有目标网络为 0.0.0.0/0 的路由规则，则参照本步骤手动配置路由规则，将私有网络流量指向 NAT 网关。

1. 在左侧导航中，选择**网络** > **路由表**。

2. 在路由表列表中，单击需要访问 Internet 的私有网络所关联的路由表 ID，进入路由表详情页。

   > **说明**
   >
   > 若私有网络还未绑定路由表，请先创建并绑定。具体操作请参见[路由表使用指导](/network/vpc/manual/routing/02_route_function/)。

3. 在**规则**页签下，点击**添加路由**。

4. 在目标网络输入框中输入规则名称及需要访问的公网 IP 地址段（如0.0.0.0/0，表示全部公网地址），下一跳选择 **NAT 网关**。

5. 点击**提交**。

6. 添加完成后，点击**应用修改**使配置生效。

### 步骤3：添加 SNAT 规则

1. 在 NAT 网关列表中，点击目标 NAT 网关的 ID 号，进入 NAT 网关详情页。

2. 在 **SNAT 规则**页签，点击**添加规则**，弹出**添加SNAT规则**窗口。

   ![](../../_images/create_snat.png)

3. 配置 SNAT 规则。
   - **名称**：SNAT 规则的名称。名称长度为1~64个字符，须由中文、英文字母、数字、下划线（_）、中划线（-）和点（.）组成。
   - **资源类型**：需要访问互联网的资源类型。选择**私有网络**表示私有网络内的全部云服务器都可以通过配置的公网 IP 访问互联网；选择**云服务器**表示所选的云服务器可以通过配置的公网 IP 访问互联网。
   - **私有网络**：**资源类型**选择**私有网络**时，需要选择一个私有网络。
   - **云服务器**：**资源类型**选择**云服务器**时，需要选择一个云服务器。
   - **公网 IP**：选择用来提供互联网访问的公网 IP。
   
4. 点击**添加**。

5. 在 NAT 网关的基本信息区域右上方点击**应用修改**使配置生效。

### 步骤4：结果验证

SNAT 规则配置成功后，您可以测试云服务器的网络连通性。

此处以 Linux 实例为例：

1. 登录[步骤3](#步骤3添加-snat-规则)中已配置 SNAT 规则的云服务器（或已配置 SNAT 规则的私有网络下任一云服务器）。

2. 执行`ping`命令，`ping`域名`www.qingcloud.com`验证公网连通性。 如果能接收到回复报文，表示连接成功。

   <img src="../../_images/ping.png" alt="ping" style="zoom:50%;" />

