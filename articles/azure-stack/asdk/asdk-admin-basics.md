---
title: Azure Stack 开发工具包基础知识 | Microsoft Docs
description: 描述如何执行基本管理任务的 Azure 堆栈开发工具包 (ASDK)。
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: 05dd42b049c75b9ea592ffe341f44e3b02b9757f
ms.sourcegitcommit: 20d103fb8658b29b48115782fe01f76239b240aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2018
---
# <a name="asdk-administration-basics"></a>ASDK 管理基础知识 
如果你不熟悉 Azure Stack 开发工具包 (ASDK) 的管理，请参考本文。 本指南概述评估环境中 Azure Stack 操作员的角色，以及如何确保测试用户快速提高工作效率。

首先请查看[什么是 Azure Stack 开发工具包？](asdk-what-is.md)一文，确保了解 ASDK 的用途和限制。 应该将开发工具包作为“沙盒”使用，在其中对 Azure Stack 进行评估，并在非生产环境中开发和测试应用。 

与 Azure 类似，Azure Stack 会快速推出创新，因此我们会定期发布 ASDK 的新版本。 但是，无法像升级 Azure Stack 集成系统部署一样升级 ASDK。 因此，若要过渡到最新版本，必须彻底[重新部署 ASDK](asdk-redeploy.md)。 不能应用更新包。 此过程需要一定的时间，但好处是可以在最新功能可用时立即试用。 

## <a name="what-account-should-i-use"></a>我应使用什么帐户?
有一些你应注意管理 Azure 堆栈时的帐户注意事项。 尤其是在部署作为标识提供程序而不是 Azure Active Directory (Azure AD) 中使用 Windows Server Active Directory 联合身份验证服务 (AD FS)。 以下的帐户注意事项适用于 Azure 堆栈集成系统和 ASDK 部署：

|帐户|Azure AD|AD FS|
|-----|-----|-----|
|本地管理员 (。 \Administrator)|ASDK 主机管理员|ASDK 主机管理员|
|AzureStack\AzureStackAdmin|ASDK 主机管理员<br><br>用于登录到 Azure 堆栈管理门户<br><br>若要查看和管理 Service Fabric 环的访问|ASDK 主机管理员<br><br>不能访问 Azure 堆栈管理门户<br><br>若要查看和管理 Service Fabric 环的访问<br><br>不再所有者的默认提供程序订阅 (DP)|
|AzureStack\CloudAdmin|可以访问并运行特权终结点中的允许的命令|可以访问并运行特权终结点中的允许的命令<br><br>可以不登录到 ASDK 主机<br><br>默认提供程序订阅 (DP) 的所有者|
|Azure AD 全局管理员|在安装期间使用<br><br>默认提供程序订阅 (DP) 的所有者|不适用|
|

## <a name="what-tools-do-i-use-to-manage"></a>使用哪些工具进行管理？
可以使用 [Azure Stack 管理员门户](https://adminportal.local.azurestack.external)或 PowerShell 来管理 Azure Stack。 若要了解基本概念，最简单的方式是使用门户。 若要使用 PowerShell，需要安装[适用于 Azure Stack 的 PowerShell](asdk-post-deploy.md#install-azure-stack-powershell) 并[从 GitHub 下载 Azure Stack 工具](asdk-post-deploy.md#download-the-azure-stack-tools)。

Azure Stack 使用 Azure 资源管理器作为其基础的部署、管理和组织机制。 若要管理 Azure Stack 并帮助支持用户，应了解 Azure 资源管理器。 有关详细信息，请参阅 [Azure 资源管理器入门白皮书](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf)。

## <a name="your-typical-responsibilities"></a>典型责任
用户需要使用服务， 从其角度来看，你的主要角色是向他们提供这些服务。 可以使用 ASDK 来了解需要提供哪些服务，以及如何通过[创建计划、产品/服务和配额](asdk-offer-services.md)来提供这些服务。 此外，需要将项（例如虚拟机映像）添加到 Marketplace。 最简单的方法是[将 Marketplace 项从 Azure 下载到 Azure Stack](asdk-marketplace-item.md)。

> [!NOTE]
> 如需测试计划、产品/服务和服务，应使用[用户门户](https://portal.local.azurestack.external)而不是[管理员门户](https://adminportal.local.azurestack.external)。

除了提供服务以外，还必须执行 Azure Stack 操作员的所有常规任务，使保持 ASDK 保持正常运行。 这些任务包括：
- 添加用于 Azure Active Directory (Azure AD) 或 Active Directory 联合身份验证服务 (AD FS) 部署的用户帐户。
- 分配基于角色的访问控制 (RBAC) 角色（不局限于管理员）
- 监视基础结构运行状况
- 管理网络和存储资源
- 更换有故障的开发工具包主机硬件 

## <a name="where-to-get-support"></a>从何处获取支持
对于开发工具包中，唯一支持的选项是支持相关在中提问[Microsoft Azure 堆栈论坛](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack)。 单击管理员门户右上角的“帮助和支持”图标（问号），然后单击“新建支持请求”，则会直接打开论坛网站。 我们会定期关注这些论坛。 

> [!IMPORTANT]
> 由于 ASDK 是一个评估环境，因此我们不会通过 Microsoft 客户支持服务 (CSS) 提供官方支持。

## <a name="next-steps"></a>后续步骤
[部署 ASDK](asdk-deploy.md)

