---
title: Identity and access management (IAM)
description: Examine design considerations and recommendations related to identity and access management in an enterprise environment.
author: BrianBlanchard
ms.author: brblanch
ms.date: 08/23/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
---

# Identity and access management

Identity provides the basis of a large percentage of security assurance. It enables access based on identity authentication and authorization controls in cloud services. These controls protect data and resources and decide which requests should be permitted.

Identity and access management (IAM) is boundary security in the public cloud. It must be treated as the foundation of any secure and fully compliant public cloud architecture. Azure offers a comprehensive set of services, tools, and reference architectures to enable organizations to make highly secure, operationally efficient environments as outlined here.

This section examines design considerations and recommendations related to IAM in an enterprise environment.

## Why we need identity and access management

The technological landscape in the enterprise environment is becoming complex and heterogenous. To manage compliance and security for this environment, IAM enables the right individuals to access the right resources at the right time for the right reasons.

### Plan for identity and access management

Enterprise organizations typically follow a least-privileged approach to operational access. This model should be expanded to consider Azure through Azure Active Directory (Azure AD), Azure role-based access control (Azure RBAC), and custom role definitions. It's critical to plan how to govern control-plane and data-plane access to resources in Azure. Any design for IAM and Azure RBAC must meet regulatory, security, and operational requirements before it can be accepted.

Identity and access management is a multistep process. It involves careful planning for identity integration and other security considerations, like blocking legacy authentication and planning for modern passwords. Staging planning also involves selection of business-to-business or business-to-consumer identity and access management. While these requirements vary, there are common design considerations and recommendations to consider for an enterprise landing zone.

![Diagram that shows identity and access management.](./media/iam.png)

*Figure 1: Identity and access management.*

**Design considerations:**

- There are limits around the number of custom roles and role assignments. These limits must be considered when you lay down a framework around IAM and governance. For more information, see [Azure RBAC service limits](/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-role-based-access-control-limits).
- There's a limit of 2,000 role assignments per subscription.
- There's a limit of 500 role assignments per management group.
- Centralized versus federated resource ownership:
  - Shared resources or any aspect of the environment that implements or enforces a security boundary, such as the network, must be managed centrally. This requirement is part of many regulatory frameworks. It's standard practice for any organization that grants or denies access to confidential or critical business resources.
  - Managing application resources that don't violate security boundaries or other aspects that are required to maintain security and compliance. These resources can be delegated to application teams. By allowing users to provision resources within a securely managed environment, organizations can make use of the agile nature of the cloud. Using this environment also prevents the violation of any critical security or governance boundary.
  - Depending on the definition of the centralized or federated resource ownership, custom roles might differ. The custom roles for the centralized resource ownership are limited and might need more rights depending on the responsibility model. For example, in some organizations a NetOps role might only need to manage and configure global connectivity. Your organization might need a more centralized approach. If so, you need to enrich the NetOps role with more allowed actions like creating peering between the hub and the spokes.

<!-- docutune:ignore Azure-AD-only Azure-AD-managed -->

**Design recommendations:**

- Use [Azure RBAC](/azure/role-based-access-control/overview) to manage data-plane access to resources where possible. Examples are Azure Key Vault, a storage account, or a SQL database.
- Deploy Azure AD conditional-access policies for any user with rights to Azure environments. Doing so provides another mechanism to help protect a controlled Azure environment from unauthorized access.
- Enforce multifactor authentication for any user with rights to the Azure environments. Multifactor authentication enforcement is a requirement of many compliance frameworks. It greatly lowers the risk of credential theft and unauthorized access.
- Use [Azure AD Privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-configure) to establish zero standing access and least privilege. Map your organization's roles to the minimum level of access needed. Azure AD PIM can be an extension of existing tools and processes, use Azure native tools as outlined, or use both as needed.
- Use Azure-AD-only groups for Azure control-plane resources in Azure AD PIM when you grant access to resources.
  - Add on-premises groups to the Azure AD only group if a group management system is already in place.
    - Add both users and groups synchronized from on-premises by using Azure AD only groups and Azure AD Connect. With this method, you can add Azure AD only users and groups to a single Azure AD only group, including guest users.
    - Groups synchronized from on-premises can only be managed and updated from the identity source of truth, like on-premises Active Directory. These groups might only contain members from the same identity source, which doesn't provide flexibility like Azure AD only groups do.
- Use Azure AD PIM access reviews to periodically validate resource entitlements. Access reviews are part of many compliance frameworks. As a result, many organizations already have a process in place to address this requirement.
- Integrate Azure AD logs with the platform-central [Log Analytics workspace](/azure/azure-monitor/logs/data-platform-logs#log-analytics-and-workspaces). It allows for a single source of truth around log and monitoring data in Azure. Using a single source of truth gives organizations cloud-native options to meet requirements around log collection and retention.
- If any data sovereignty requirements exist, custom user policies can be deployed to enforce them.
- Use custom role definitions within the Azure AD tenant while you consider the following key roles:

| Role | Usage | Actions | No actions |
|---|---|---|---|
| Azure platform owner (such as the built-in Owner role)               | Management group and subscription lifecycle management                                                           | `*`                                                                                                                                                                                                                  |                                                                                                                                                                                         |
| Network management (NetOps)        | Platform-wide global connectivity management: Virtual networks, UDRs, NSGs, NVAs, VPN, Azure ExpressRoute, and others            | `*/read`, `Microsoft.Network/*`, `Microsoft.Resources/deployments/*`, `Microsoft.Support/*`                            |                                                                                                                                                                               |
| Security operations (SecOps)       | Security administrator role with a horizontal view across the entire Azure estate and the Azure Key Vault purge policy | `*/read`, `*/register/action`, `Microsoft.KeyVault/locations/deletedVaults/purge/action`, `Microsoft.PolicyInsights/*`, `Microsoft.Authorization/policyAssignments/*`, `Microsoft.Authorization/policyDefinitions/*`, `Microsoft.Authorization/policyExemptions/*`, `Microsoft.Authorization/policySetDefinitions/*`, `Microsoft.Insights/alertRules/*`, `Microsoft.Resources/deployments/*`, `Microsoft.Security/*`, `Microsoft.Support/*` |                                                                            |
| Subscription owner                 | Delegated role for subscription owner derived from subscription Owner role                                       | `*`                                                                                                                                                                                                                  | `Microsoft.Authorization/*/write`, `Microsoft.Network/vpnGateways/*`, `Microsoft.Network/expressRouteCircuits/*`, `Microsoft.Network/routeTables/write`, `Microsoft.Network/vpnSites/*` |
| Application owners (DevOps/AppOps) | Contributor role granted for application/operations team at resource group level                                 | `*`                                                                                                                                                                                                                   | `Microsoft.Authorization/*/write`, `Microsoft.Network/publicIPAddresses/write`, `Microsoft.Network/virtualNetworks/write`, `Microsoft.KeyVault/locations/deletedVaults/purge/action`                                         |

- Use Microsoft Defender for Cloud just-in-time access for all infrastructure as a service (IaaS) resources to enable network-level protection for ephemeral user access to IaaS virtual machines.
- Use Azure AD managed identities for Azure resources to avoid authentication based on user names and passwords. Because many security breaches of public cloud resources originate with credential theft embedded in code or other text sources, enforcing managed identities for programmatic access greatly reduces the risk of credential theft.
- Use privileged identities for automation runbooks that require elevated access permissions. Automated workflows that violate critical security boundaries should be governed by the same tools and policies users of equivalent privilege are.
- Don't add users directly to Azure resource scopes. Instead add users to defined roles, which are then assigned to resource scopes. Direct user assignments circumvent centralized management, greatly increasing the management required to prevent unauthorized access to restricted data.

### Plan for authentication inside a landing zone

An important design decision an enterprise must make when adopting Azure is whether to extend an existing on-premises identity domain into Azure or to create a brand new one. Assess requirements for authentication inside the landing zone. Then incorporate them into plans to deploy Active Directory Domain Services (AD DS) in Windows Server, Azure AD Domain Services (Azure AD DS), or both. Most Azure environments use at least Azure AD for Azure fabric authentication and AD DS local host authentication and group policy management.

**Design considerations:**

- Consider centralized and delegated responsibilities to manage resources deployed inside the landing zone.
- Applications that rely on domain services and use older protocols can use [Azure AD DS](/azure/active-directory-domain-services/).
- There's a difference between Azure AD, Azure AD DS, and AD DS running on Windows Server. Evaluate your application needs, and understand and document the authentication provider that each one will be using. Plan correctly for all applications.

**Design recommendations:**

- Use centralized and delegated responsibilities to manage resources deployed inside the landing zone based on role and security requirements.
- Privileged operations require special permissions. These operations include:

  - Creating service principal objects.
  - Registering applications in Azure AD.
  - Getting and handling certificates or wildcard certificates.

  Consider which users will handle such requests. Then consider how to secure and monitor their accounts with the degree of diligence required.
- If an organization has a scenario where an application that uses integrated Windows authentication must be accessed remotely through Azure AD, consider using [Azure AD Application Proxy](/azure/active-directory/app-proxy/application-proxy).
- Evaluate the compatibility of workloads for AD DS on Windows Server and for Azure AD DS.
- Ensure your network design allows resources that require AD DS on Windows Server for local authentication and management to access the appropriate domain controllers.
  - For AD DS on Windows Server, consider shared services environments that offer local authentication and host management in a larger enterprise-wide network context.
- Deploy Azure AD DS within the primary region because this service can only be projected into one subscription. The Azure AD DS-managed domain can be expanded to further regions with [replica sets](/azure/active-directory-domain-services/concepts-replica-sets).
- Use managed identities instead of service principals for authentication to Azure services. This approach reduces exposure to credential theft.
