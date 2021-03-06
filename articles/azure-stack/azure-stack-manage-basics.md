---
title: Azure Stack administration basics | Microsoft Docs
description: Learn what you need to know to administer Azure Stack.
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 856738a7-1510-442a-88a8-d316c67c757c
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: twooley
ms.translationtype: HT
ms.sourcegitcommit: 8b857b4a629618d84f66da28d46f79c2b74171df
ms.openlocfilehash: c62b4c165cdeeb0a038521ad9e43e061044c921c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/04/2017

---
# <a name="azure-stack-administration-basics"></a>Azure Stack administration basics

There are several things you need to know if you're new to Azure Stack administration. This guidance provides an overview of your role as a cloud operator, and what you need to tell your users for them to become productive quickly.

## <a name="understand-development-kit-builds"></a>Understand development kit builds

Review the [What is Azure Stack?](azure-stack-poc.md) article to make sure you understand the purpose of the Azure Stack Development Kit, and its limitations. You should use the development kit as a "sandbox," where you can evaluate Azure Stack, and develop and test your apps in a non-production environment. (For deployment information, see the [Azure Stack Development Kit deployment](azure-stack-deploy-overview.md) quickstart.)

Like Azure, we innovate rapidly. We'll regularly release new builds. When you want to move to the latest build, you must [redeploy Azure Stack](azure-stack-redeploy.md). This process takes time, but the benefit is that you can try out the latest features. The documentation on our website reflects the latest release build.

## <a name="learn-about-available-services"></a>Learn about available services

You'll need an awareness of which services you can make available to your users. Azure Stack supports a subset of Azure services. The list of supported services will continue to evolve.

**Foundational services**

By default, Azure Stack includes the following "foundational services" when you deploy Azure Stack:

- Compute
- Storage
- Networking
- Key Vault

With these foundational services, you can offer Infrastructure-as-a-Service (IaaS) to your users with minimal configuration.

**Additional services**

Currently, we support the following additional Platform-as-a-Service (PaaS) services:

- App Service
- Azure Functions
- SQL and MySQL databases

These services require additional configuration before you can make them available to your users. For more information, see the "Tutorials" and the "How-to guides\Offer services" sections of our documentation.

**Service roadmap**

Azure Stack will continue to add support for Azure services. For the projected roadmap, see the [Hybrid Application Innovation with Azure and Azure Stack](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409) whitepaper. You can also monitor the [Azure Stack blog posts](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview) for new announcements.

## <a name="what-tools-do-i-use-to-manage"></a>What tools do I use to manage?
 
You can use the [administrator portal](azure-stack-manage-portals.md) or PowerShell to manage Azure Stack. The easiest way to learn the basic concepts is through the portal. If you want to use PowerShell, there are preparation steps. You must [install](azure-stack-powershell-install.md) PowerShell, [download](azure-stack-powershell-download.md) additional modules, and [configure](azure-stack-powershell-configure.md) PowerShell.

Azure Stack uses Azure Resource Manager as its underlying deployment, management, and organization mechanism. If you're going to manage Azure Stack and help support users, you should learn about Resource Manager. See the [Getting Started with Azure Resource Manager](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf) whitepaper.

## <a name="your-typical-responsibilities"></a>Your typical responsibilities

Your users want to use services. From their perspective, your main role is to make these services available to them. You must decide which services to offer, and make those services available by creating [quotas](azure-stack-setting-quotas.md), [plans](azure-stack-create-plan.md), and [offers](azure-stack-create-offer.md). 

You'll also need to add items to the marketplace, such as virtual machine images. The easiest way is to [download marketplace items from Azure to Azure Stack](azure-stack-download-azure-marketplace-item.md).

> [!NOTE]
> If you want to test your plans, offers, and services, you should use the [user portal](azure-stack-manage-portals.md); not the administrator portal.

In addition to providing services, you must perform all the regular  duties of a cloud operator to keep Azure Stack up and running. These duties include the following:

- Add user accounts (for [Azure Active Directory](azure-stack-add-new-user-aad.md) deployment or for [Active Directory Federation Services](azure-stack-add-users-adfs.md) deployment)
- [Assign role-based access control (RBAC) roles](azure-stack-manage-permissions.md) (This is not restricted to administrators.)
- [Monitor infrastructure health](azure-stack-monitor-health.md)
- Manage [network](azure-stack-viewing-public-ip-address-consumption.md) and [storage](azure-stack-manage-storage-accounts.md) resources
- Replace bad hardware

## <a name="what-to-tell-your-users"></a>What to tell your users

You'll need to let your users know how to work with services in Azure Stack, how to connect to the development kit environment, and how to subscribe to offers.

**Understand how to work with services in Azure Stack**

There's information your users must understand before they use services and build apps in Azure Stack. For example, there are specific PowerShell and API version requirements. Also, there are some feature deltas between a service in Azure and the equivalent service in Azure Stack. Make sure that your users review the following articles:

- [Key considerations: Using services or building apps for Azure Stack](azure-stack-considerations.md)
- [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md)
- [Storage: differences and considerations](azure-stack-acs-differences-tp2.md)

The information in these articles summarizes the differences between a service in Azure and Azure Stack. It supplements the information that's available for an Azure service in the global Azure documentation. 

**Connect to Azure Stack as a user**

In a development kit environment, if a user doesn't have Remote Desktop access to the development kit host, they must configure a virtual private network (VPN) connection before they can access Azure Stack. See [Connect to Azure Stack](azure-stack-connect-azure-stack.md). 

Your users will want to know how to [access the user portal ](azure-stack-manage-portals.md) or how to connect through PowerShell. If using PowerShell, users may have to register resource providers before they can use services. (A resource provider manages a service. For example, the networking resource provider manages resources such as virtual networks, network interfaces, and load balancers.) They must [install](azure-stack-powershell-install.md) PowerShell, [download](azure-stack-powershell-download.md) additional modules, and [configure](azure-stack-powershell-configure.md) PowerShell (which includes resource provider registration).

**Subscribe to an offer**

Before a user can access services, they must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that you've created as a cloud operator.

## <a name="where-to-get-support"></a>Where to get support

For the Azure Stack Development Kit, you can ask support-related questions in the [Microsoft forums](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack). If you click the Help and support icon (question mark) in the upper-right corner of the administrator portal, and then click **New support request**, this opens the forums site directly. These forums are regularly monitored. Because the development kit is an evaluation environment, there is no official support offered through Microsoft Customer Support Services (CSS).

## <a name="next-steps"></a>Next steps

- [Region management in Azure Stack](azure-stack-region-management.md)



