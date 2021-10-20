---
title: "使用 Web Installer 安装"
description: 本小节主要介绍青立方® 超融合易捷版 使用 Web Installer 安装。 
keywords: 使用 Web Installer 安装,
weight: 20
collapsible: false
draft: false
---

青立方® 超融合易捷版采用 Web Installer 对待安装机器及部署流程进行可视化部署，以极简的 **Step-by-Step** 安装方式引导用户快速配置节点安装环境。

本示例准备了 IP 地址为 172.16.76.3 - 172.16.76.5 共 3 台机器用于演示，满足最小安装要求。

## 前提条件

- 已登录 Web Installer。

## 步骤 1：基本信息

在基本信息中，可根据实际环境自定义域名、区域 ID、控制台名称、网络协议、管理网络范围，本安装示例填写的信息如下：

- **域名**：即 青立方® 超融合易捷版在浏览器中最终的访问地址，例如 expresscloud.com。

- **区域 ID**：可自定义区域 ID 值，没有规则限制，为方便理解可设置如 pek3 (北京 3 区)，gd2 (广东 2 区)。

- **控制台名**称：可自定义易捷版控制台界面的名称，例如青云易捷版。
  
- **网络协议**：此处默认采用 http。

- **管理网络范围**：此处输入待安装机器可管理的网段地址。本示例为 172.16.76.3-172.16.76.200，例如待安装机器的起始 IP 地址为 172.16.76.3，则管理网络范围的区间可位于 172.16.76.3-172.16.76.254 区间，需保证该范围中部分网段未被占用。

![基本信息](../../_images/basic_info.png)

## 步骤 2：节点设置

1. 节点设置中，需添加至少 3 个节点，并且保证 seed,  vbr 及 snapshot 角色的个数分别不少于 2 个才可满足最小安装要求，点击 **添加节点**。

2. 在弹窗中，输入预先准备的 3 台 IP 地址连续的机器 IP 段：172.16.76.3 - 5，完成后点击 **扫描可用节点**。

    > **注意**
    > 
    > 安装程序将自动过滤掉用户所输入 IP 段中空缺的 IP，如果准备了 4 台节点 172.16.76.3 - 172.16.76.5 和 172.16.76.7，直接输入 172.16.76.3 - 7 即可扫描到这四台节点。

    ![节点设置](../../_images/config_node_1.png)

3. 在节点设置中可以看到扫描到的可用节点，即当前准备的 3 台机器以及待安装机器的节点角色和节点信息，默认无需修改节点角色。

    ![节点设置](../../_images/config_node_2.png)

4. 点击 **编辑节点**，进入查看节点的详情，其中磁盘类型支持混合。注意，请进入每一个节点检查其默认的数据盘类型，必须保证 每个节点的数据盘至少有一块 SSD 类型的磁盘，否则安装可能会失败。验证完毕后，点击右上角关闭按钮将自动保存生效。

    ![节点设置](../../_images/config_node_3.png)

## 步骤 3：可选服务

根据需要选装 QingCloud 桌面云 和V2V 迁移工具，QingCloud 桌面云 提供企业级的桌面云服务，QingCloud 桌面云是基于 QingCloud IaaS 平台研发的新一代企业级办公解决方案。

V2V 迁移工具提供静态迁移能力，可将其它云平台（vmware、Xen）等的虚拟主机系统及数据通过 WEB 上传的方式拷贝到当前平台目的主机。

![可选服务](../../_images/other_service.png)

## 步骤 4：安装 & 预览

1. 检查安装预览页中的基本信息和节点设置信息，确认无误后点击 **安装**，配置和部署步骤将自动进行。

    > **注意**
    > 
    > 安装过程中如果关闭了浏览器或者相应的安装页面，安装过程在后台仍将继续执行，重新打开该页面，即可回到刚才的安装部署状态。

   ![检查安装配置](../../_images/check_config.png)

   ![安装中](../../_images/installing.png)

2. 若节点配置正确且安装过程中未报错，即安装成功。

3. 进入运维管理的基本信息页面，试用 License 默认一个月，需要在到期前输入新的 License 激活产品。点击**点击访问**通过访问地址访问 Console 页面。

    > **注意**
    > 
    > 此时需要将访问地址下的所有 hosts 记录添加到本地的 hosts 文件中。使用 Windows 进行访问的用户，可在 `c:\windows\system32\drivers\etc\hosts` 文件中添加。使用 Linux 和 Mac OS 访问的用户，可在 `/etc/hosts` 文件中添加。

   ![License](../../_images/license.png)

4. 访问内网域名 console.expresscloud.com 即可打开 青立方® 超融合易捷版登录页面。

    **用户名**：admin@domain (domain 是在第一步基本信息中用户设置的域名，例如本示例是 admin@expresscloud.com)
    
    **密码**：zhu88jie

    > **注意**
    > 
    > 选装了桌面云后，可通过域名 desktop.expresscloud.com 来访问，默认使用 admin / zhu88jie 登录。部署桌面云应用后，可使用桌面云的 desktop@expresscloud.com / zhu88jie 账号登录 青立方® 超融合易捷版管理桌面云的资源。

   ![访问](../../_images/access.png)