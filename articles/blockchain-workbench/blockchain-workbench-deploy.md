---
title: 部署 Azure Blockchain Workbench
description: 如何部署 Azure Blockchain Workbench
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 4/22/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: 85a627678f862d783d47013d82bae8b485d7d4e9
ms.sourcegitcommit: e14229bb94d61172046335972cfb1a708c8a97a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2018
---
# <a name="deploy-azure-blockchain-workbench"></a>部署 Azure Blockchain Workbench

Azure Blockchain Workbench 是使用 Azure Marketplace 中的解决方案模板部署的。 该模板可以简化创建区块链应用程序所需的组件的部署。 部署后，Blockchain Workbench 提供对客户端应用的访问权限，以创建和管理用户与区块链应用程序。

有关 Blockchain Workbench 组件的详细信息，请参阅 [Azure Blockchain Workbench 体系结构](blockchain-workbench-architecture.md)。

## <a name="prepare-for-deployment"></a>准备部署

在部署之前，Azure Blockchain Workbench 要求满足几项先决条件。 先决条件包括 Azure AD 配置和应用程序注册。

### <a name="blockchain-workbench-api-app-registration"></a>Blockchain Workbench API 应用注册

Blockchain Workbench 部署要求注册 Azure AD 应用程序。 需要使用 Azure Active Directory (Azure AD) 来注册应用。 可以使用现有租户，也可以创建新租户。 如果使用现有的 Azure AD 租户，需要拥有足够的权限才能在 Azure AD 租户中注册应用程序。 应用程序注册需要在部署 Workbench 的订阅的订阅管理员租户中进行。 有关 Azure AD 租户的详细信息，请参阅[如何获取 Active Directory 租户](../active-directory/develop/active-directory-howto-tenant.md)和[将应用程序与 Azure Active Directory 集成](../active-directory/develop/active-directory-integrating-applications.md)。

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 在右上角选择自己的帐户，然后切换到所需的 Azure AD 租户。 该租户应是部署 Workbench 的订阅的订阅管理员租户，并且你有足够的权限在其中注册应用程序。
3. 在左侧导航窗格中，选择“Azure Active Directory”服务。 选择“应用注册” > “新建应用程序注册”。

    ![应用注册](media/blockchain-workbench-deploy/app-registration.png)

4. 提供应用程序的“名称”和“登录 URL”。 可以使用占位符值，因为在部署期间会更改这些值。 

    ![创建应用注册](media/blockchain-workbench-deploy/app-registration-create.png)

    |设置  | 值  |
    |---------|---------|
    |名称 | `Blockchain API` |
    |应用程序类型 |Web 应用/API|
    |登录 URL | `https://blockchainapi` |

5. 选择“创建”以注册 Azure AD 应用程序。

### <a name="modify-application-manifest"></a>修改应用程序清单

接下来，需将应用程序清单修改为使用 Azure AD 中的应用程序角色，以指定 Blockchain Workbench 管理员。  有关应用程序清单的详细信息，请参阅 [Azure Active Directory 应用程序清单](../active-directory/develop/active-directory-application-manifest.md)。

1. 针对已注册的应用程序，在其详细信息窗格中选择“清单”。
2. 生成 GUID。 可以使用 PowerShell 命令 `[guid]::NewGuid()` 或联机工具来生成 GUID。 
3. 稍后将要更新清单的 **appRoles** 节。 在“编辑清单”窗格中选择“编辑”，将 `"appRoles": []` 替换为所提供的 JSON。 请务必将 **id** 字段的值替换为生成的 GUID。 

    ``` json
    "appRoles": [
         {
           "allowedMemberTypes": [
             "User",
             "Application"
           ],
           "displayName": "Administrator",
           "id": "<A unique GUID>",
           "isEnabled": true,
           "description": "Blockchain Workbench administrator role allows creation of applications, user to role assignments, etc.",
           "value": "Administrator"
         }
       ],
    ```

    ![编辑清单](media/blockchain-workbench-deploy/edit-manifest.png)

    > [!IMPORTANT]
    > 需要使用“管理员”值来标识 Blockchain Workbench 管理员。

4.  单击“保存”以保存对应用程序清单所做的更改。

### <a name="add-graph-api-required-permissions"></a>添加图形 API 所需的权限

API 应用程序需要从用户请求目录访问权限。 为 API 应用程序设置以下所需权限：

1. 在区块链 API 应用注册中，选择“设置”>“所需的权限”>“选择 API”>“Microsoft Graph”。

    ![选择 API](media/blockchain-workbench-deploy/client-app-select-api.png)

    单击“选择”。

2. 在“应用程序权限”下面的“启用访问权限”中，选择“读取所有用户的完整个人资料”。

    ![启用访问权限](media/blockchain-workbench-deploy/client-app-read-perms.png)

    依次单击“选择”、“完成”。

3. 在“所需的权限”中选择“授予权限”，然后在出现验证提示时选择“是”。

   ![授予权限](media/blockchain-workbench-deploy/client-app-grant-permissions.png)

   授予权限可让 Blockchain Workbench 访问目录中的用户。 在 Blockchain Workbench 中搜索和添加成员需有读取权限。

### <a name="add-graph-api-key-to-application"></a>将图形 API 密钥添加到应用程序

针对与区块链应用程序交互的用户，Blockchain Workbench 使用 Azure AD 作为主要标识管理系统。 为使 Blockchain Workbench 能够访问 Azure AD 和检索用户信息（例如名称和电子邮件），需要添加访问密钥。 Blockchain Workbench 使用该密钥在 Azure AD 中进行身份验证。

1. 针对已注册的应用程序，在其详细信息窗格中选择“设置”。
2. 选择“密钥”。
3. 添加新密钥：指定密钥**说明**，并选择**过期**期限值。 

    ![创建密钥](media/blockchain-workbench-deploy/app-key-create.png)

    |设置  | 值  |
    |---------|---------|
    | 说明 | `Service` |
    | Expires | 选择过期期限 |

4. 选择“保存”。 
5. 复制并存储密钥值， 稍后需要将它用于部署。

    > [!IMPORTANT]
    >  如果未保存部署用的密钥，则需要生成新密钥。 稍后无法从门户检索密钥值。

### <a name="get-application-id"></a>获取应用程序 ID

部署时需要应用程序 ID 和租户信息。 请收集并存储这些信息，以便在部署期间使用。

1. 针对已注册的应用程序，选择“设置” > “属性”。
2.  在“属性”窗格中，复制并存储以下值，以便稍后在部署期间使用。

    ![API 应用属性](media/blockchain-workbench-deploy/app-properties.png)

    | 要存储的设置  | 在部署中使用 |
    |------------------|-------------------|
    | 应用程序 ID | “Azure Active Directory 设置”>“应用程序 ID” |

### <a name="get-tenant-domain-name"></a>获取租户域名

收集并存储要在其中注册应用程序的 Active Directory 租户域名。 

在左侧导航窗格中，选择“Azure Active Directory”服务。 选择“自定义域名”。 复制并存储域名。

![域名](media/blockchain-workbench-deploy/domain-name.png)

## <a name="deploy-blockchain-workbench"></a>部署 Blockchain Workbench

完成先决条件步骤后，便可以部署 Blockchain Workbench。 以下部分概述了如何部署框架。

1.  登录到 [Azure 门户](https://portal.azure.com)。
2.  在右上角选择自己的帐户，然后切换到要在其中部署 Azure Blockchain Workbench 的所需 Azure AD 租户。
3.  在左窗格中，选择“创建资源”。 在“搜索 Marketplace”搜索栏中搜索 `Azure Blockchain Workbench`。 

    ![Marketplace 搜索栏](media/blockchain-workbench-deploy/marketplace-search-bar.png)

4.  选择“Azure Blockchain Workbench”。

    ![Marketplace 搜索结果](media/blockchain-workbench-deploy/marketplace-search-results.png)

4.  选择**创建**。
5.  完成基本设置。

    ![创建 Azure Blockchain Workbench](media/blockchain-workbench-deploy/blockchain-workbench-settings-basic.png)

    | 设置 | 说明  |
    |---------|--------------|
    | 资源前缀 | 部署的短唯一标识符。 此值用作资源命名的基础。 |
    | VM 用户名 | 该用户名用作所有虚拟机 (VM) 的管理员。 |
    | 身份验证类型 | 选择是要使用密码还是密钥连接到 VM。 |
    | 密码 | 使用密码连接到 VM。 |
    | SSH | 使用单行格式（以 **ssh-rsa** 开头）的 RSA 公钥，或使用多行 PEM 格式。 可以在 Linux 和 OS X 上使用 `ssh-keygen` 生成 SSH 密钥，或在 Windows 上使用 PuTTYGen 生成这些密钥。 有关 SSH 密钥的详细信息，请参阅[如何在 Azure 上的 Windows 中使用 SSH 密钥](../virtual-machines/linux/ssh-from-windows.md)。 |
    | 数据库密码/确认数据库密码 | 指定密码，用于访问在部署过程中创建的数据库。 |
    | 部署区域 | 指定部署 Blockchain Workbench 资源的位置。 为了尽可能提高可用性，此位置应与“位置”设置相符。 |
    | 订阅 | 指定要用于部署的 Azure 订阅。 |
    | 资源组 | 选择“新建”创建新资源组，并指定唯一的资源组名称。 |
    | Location | 指定要将框架部署到的区域。 |

6.  选择“确定”完成基本设置配置部分。

7.  完成“Azure Active Directory 设置”。

    ![Azure AD 设置](media/blockchain-workbench-deploy/blockchain-workbench-settings-aad.png)

    | 设置 | 说明  |
    |---------|--------------|
    | 域名 | 使用在[获取租户域名](#get-tenant-domain-name)先决条件部分中收集的 Azure AD 租户。 |
    | 应用程序 ID | 使用在[获取应用程序 ID](#get-application-id) 先决条件部分中收集的、区块链客户端应用注册中的应用程序 ID。 |
    | 应用程序密钥 | 使用在[将图形 API 密钥添加到应用程序](#add-graph-api-key-to-application)先决条件部分中收集的、区块链客户端应用注册中的应用程序密钥。 |


8.  单击“确定”完成“Azure AD 参数”配置部分。

9.  完成“网络大小和性能”设置。

    ![网络和性能设置](media/blockchain-workbench-deploy/blockchain-workbench-settings-network.png)

    | 设置 | 说明  |
    |---------|--------------|
    | 区块链节点数 | 选择要在网络中部署的 Ethereum PoA 验证程序节点数。 |
    | 存储性能 | 为区块链网络选择首选的 VM 存储性能。 |
    | 虚拟机大小 | 为区块链网络选择首选的 VM 大小。 |

10. 选择“确定”，完成网络大小和性能部分。

11. 完成“Azure Monitor”设置。

    ![Azure Monitor](media/blockchain-workbench-deploy/blockchain-workbench-settings-oms.png)

    | 设置 | 说明  |
    |---------|--------------|
    | 监视 | 选择是否要允许 Azure Monitor 监视区块链网络 |
    | 连接到现有的 Log Analytics 实例 | 选择是要使用现有的 Log Analytics 实例，还是创建新实例。 如果使用现有的实例，请输入工作区 ID 和主密钥。 |

12. 单击“确定”完成“Azure Monitor”部分。

13. 查看摘要，验证参数是否准确。

    ![摘要](media/blockchain-workbench-deploy/blockchain-workbench-summary.png)

14. 选择“创建”并同意条款，以部署 Azure Blockchain Workbench。

部署最长可能需要花费 90 分钟。 可以使用 Azure 门户监视进度。 在新建的资源组中，选择“部署”>“概述”查看已部署项目的状态。

## <a name="blockchain-workbench-web-url"></a>Blockchain Workbench Web URL

完成 Blockchain Workbench 的部署后，某个新资源组会包含你的 Blockchain Workbench 资源。 通过 Web URL 访问 Blockchain Workbench 服务。 以下步骤说明如何检索已部署框架的 Web URL。

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 在左侧导航窗格中，选择“资源组”
3. 选择部署 Blockchain Workbench 时指定的资源组名称。
4. 单击“类型”列标题，按类型的字母顺序将列表排序。
5. 有两个类型为“应用服务”的资源。 选择类型为“应用服务”且不带“-api”后缀的资源。

    ![应用服务列表](media/blockchain-workbench-deploy/resource-group-list.png)

6.  在应用服务的“概要”部分复制“URL”值，该值表示已部署的 Blockchain Workbench 的 Web URL。

    ![应用服务概要](media/blockchain-workbench-deploy/app-service.png)

若要将自定义域名与 Blockchain Workbench 相关联，请参阅[使用流量管理器为 Azure 应用服务中的 Web 应用配置自定义域名](../app-service/web-sites-traffic-manager-custom-domain-name.md)。

## <a name="configuring-the-reply-url"></a>配置回复 URL

部署 Azure Blockchain Workbench 后，下一步是确保将 Azure Active Directory (Azure AD) 客户端应用程序注册到已部署 Blockchain Workbench Web URL 的正确**回复 URL**。

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 验证是否位于 Azure AD 客户端应用程序所注册到的租户中。
3. 在左侧导航窗格中，选择“Azure Active Directory”服务。 选择“应用注册”。
4. 选择在先决条件部分中注册的 Azure AD 客户端应用程序。
5. 选择“设置”>“回复 URL”。
6. 指定在**获取 Azure Blockchain Workbench Web URL** 部分中检索到的 Azure Blockchain Workbench 部署主要 Web URL。 回复 URL 带有 `https://` 前缀。 例如： `https://myblockchain2-7v75.azurewebsites.net`

    ![回复 URL](media/blockchain-workbench-deploy/configure-reply-url.png)

7. 选择“保存”更新客户端注册。

## <a name="next-steps"></a>后续步骤

本操作指南文章介绍了如何部署 Azure Blockchain Workbench。 若要了解如何创建区块链应用程序，请继续学习下一篇操作指南文章。

> [!div class="nextstepaction"]
> [在 Azure Blockchain Workbench 中创建区块链应用程序](blockchain-workbench-create-app.md)