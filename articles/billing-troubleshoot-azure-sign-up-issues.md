---
title: "排查 Azure 注册问题 | Microsoft Docs"
description: "说明如何解决某些常见的 Azure 注册问题。"
services: 
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: cjiang
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: e2e22b767ce1d54e7b90158fb6adb877e3a165b8


---
# <a name="i-cant-sign-up-for-azure"></a>不能注册 Azure
如果无法注册 Azure，可以通过几种方法来检查并解决此问题。

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>注册帐户验证过程中没有收到短信或电话
* 请确认你的电话号码可以接收短信。
* 再次确认你输入的电话号码，包括下拉菜单中的国家/地区代码选择。
* 请确保你的电话可以接收短信 (SMS)（如果使用“发送短信”）或接听来电（如果选择“呼叫我”替代项）。
* 如果使用手机，请确保手机连接通畅。
* 如果选择“发送短信”，最多等候 4 分钟，消息传送系统就会将文本代码发送给你。
* 收到短信后，请在文本框中插入代码，然后单击“验证”按钮以继续。

### <a name="suggestions"></a>建议
* 如果你的电话未收到短信 (SMS)，请使用“呼叫我”替代验证方法。
* 如果使用短信和“呼叫我”方法的电话验证步骤均失败，请使用其他电话号码。
* 电话验证过程中不能使用 VOIP 电话号码。

> [!NOTE]
> 可以稍后通过[更新个人资料信息](billing-how-to-change-azure-account-profile.md)更改首选电话号码。
> 
> 

## <a name="credit-card-declined-or-not-accepted"></a>信用卡被拒绝或不被接受
请确保注册时使用的付款方式是 Azure 激活或付款所支持的方式。

* 不接受虚拟和预付信用卡/借记卡。
* 根据帐户所属的国家/地区，接受的信用卡/借记卡提供商会有所不同。

### <a name="suggestion"></a>建议
有关使用信用卡或借记卡出现的注册问题的常见原因，请参阅[信用卡或借记卡在注册 Azure 时被拒绝](billing-credit-card-fails-during-azure-sign-up.md)。

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>无法激活 MSDN、BizSpark、BizSparkPlus 或 MPN 等 Azure 权益计划
通过权益计划渠道验证你是否符合所选计划的资格：

* MSDN
  * 在 [MSDN 帐户页](https://msdn.microsoft.com/subscriptions/manage/default.aspx)中验证资格状态。
  * 如果无法验证资格状态，请联系 [MSDN 订阅客服中心](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* MPN
  * 登录到 [MPN 门户](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx)并验证资格状态。 如果拥有相应的[云平台能力](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx)，可能会符合其他权益的资格。
  * 如果无法验证资格状态，请联系 [MPN 支持](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx)。
* Bizpark
  * 登录到 [BizSpark 门户](https://www.microsoft.com/bizspark/default.aspx#start-two)，然后验证 BizSpark 和 BizSpark Plus 的资格状态。
  * 如果无法验证资格状态，请向 BizSpark 团队发送电子邮件，以[联系 BizSpark 支持](mailto:bizspark@microsoft.com?subject=BizSpark%20Support&body=Thank%20you%20for%20contacting%20BizSpark.%20Please%20provide%20as%20much%20of%20the%20following%20information%20as%20possible,%20as%20it%20will%20help%20expedite%20our%20response%20to%20you.%0aContact%20name:%0aStartup%20name:%0aMicrosoft%20Account/Live%20ID:%0aSpecific%20description%20of%20issue%20experienced%20or%20question:%0a%0aThank%20you,%0a%0aThe%20BizSpark%20Team)

### <a name="suggestion"></a>建议
如果尝试激活新的权益订阅，但在注册期间遇到错误，请确保已在 [Azure 订阅页](http://account.windowsazure.com/Subscriptions)完成订阅设置。 可能需要几分钟，订阅才会显示为活动状态。 订阅激活之后，会收到电子邮件。 如果订阅状态持续挂起超过四分钟，请[联系 Azure 支持](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409)获取帮助。

## <a name="cant-activate-new-azure-in-open-subscription"></a>无法激活新的 Azure 开放许可订阅
必须具备有效的 OSA 密钥以及至少一个与之关联的 Azure 开放许可令牌，才能激活新的 Azure 开放许可订阅。

### <a name="suggestion"></a>建议
如果没有 OSA 密钥，请联系 [Microsoft Pinpoint](http://pinpoint.microsoft.com/) 中列出的其中一个 Microsoft 合作伙伴。

## <a name="cant-activate-azure-free-trial"></a>无法激活 Azure 免费试用版
是否曾经使用过 Azure 订阅？ Azure 使用条款协议仅向 Azure 新用户授予免费试用版激活权限。 如果已拥有任何其他类型的 Azure 订阅，则无法激活免费试用版。

### <a name="suggestion"></a>建议
* 如果以前激活过 Azure 订阅并且免费试用版激活失败，请考虑使用即用即付订阅。 
* 查看是否有资格使用权限产品/服务。 若要了解详细信息，请参阅 [Microsoft Azure 产品/服务详细信息页](https://azure.microsoft.com/support/legal/offer-details/)。 权益计划需要特定的先决条件。

## <a name="need-help-contact-support"></a>需要帮助？ 联系支持人员。
如果仍需帮助，请[联系支持人员](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解决问题。 




<!--HONumber=Nov16_HO3-->

