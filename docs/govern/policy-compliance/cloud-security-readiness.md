---
title: CISO cloud security readiness guide
description: Prepare the chief information security office (CISO) for cloud transformation and incremental governance.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: internal
---

# CISO cloud readiness guide

Microsoft guidance like the Cloud Adoption Framework is not positioned to determine or guide the unique security constraints of the thousands of enterprises supported by this documentation. When moving to the cloud, the role of the chief information security officer or chief information security office (CISO) isn't supplanted by cloud technologies. Quite the contrary, the CISO and the office of the CISO, become more engrained and integrated. This guide assumes the reader is familiar with CISO processes and is seeking to modernize those processes to enable cloud transformation.

Cloud adoption enables services that weren't often considered in traditional IT environments. Self-service or automated deployments are commonly executed by application development or other IT teams not traditionally aligned to production deployment. In some organizations, business constituents similarly have self-service capabilities. This can trigger new security requirements that weren't needed in the on-premises world. Centralized security is more challenging, security often becomes a shared responsibility across the business and IT culture. This article can help a CISO prepare for that approach and engage in incremental governance.

## How can a CISO prepare for the cloud?

Like most policies, security and governance policies within an organization tend to grow organically. When security incidents happen, they shape policy to inform users and reduce the likelihood of repeat occurrences. While natural, this approach creates policy bloat and technical dependencies. Cloud transformation journeys create a unique opportunity to modernize and reset policies. While preparing for any transformation journey, the CISO can create immediate and measurable value by serving as the primary stakeholder in a [policy review](./cloud-policy-review.md).

In such a review, the role of the CISO is to create a safe balance between the constraints of existing policy/compliance and the improved security posture of cloud providers. Measuring this progress can take many forms, often it's measured in the number of security policies that can be safely offloaded to the cloud provider.

**Transferring security risks:** As services are moved into infrastructure as a service (IaaS) hosting models, the business assumes less direct risk regarding hardware provisioning. The risk isn't removed, instead it's transferred to the cloud vendor. Should a cloud vendor's approach to hardware provisioning provide the same level of risk mitigation, in a secure repeatable process, the risk of hardware provisioning execution is removed from corporate IT's area of responsibility and transferred to the cloud provider. This reduces the overall security risk that corporate IT is responsible for managing, although the risk itself should still be tracked and reviewed periodically.

As solutions move further up the stack to incorporate platform as a service (PaaS) or software as a service (SaaS) models, additional risks can be avoided or transferred. When risk is safely moved to a cloud provider, the cost of executing, monitoring, and enforcing security policies or other compliance policies can be safely reduced as well.

**Growth mindset:** Change can be scary to both the business and technical implementors. When the CISO leads a growth mindset shift in an organization, we've found that those natural fears are replaced with an increased interest in safety and policy compliance. Approaching a [policy review](./cloud-policy-review.md), a transformation journey, or simple implementation reviews with a growth mindset, allows the team to move quickly but not at the cost of a fair and manageable risk profile.

## Resources for the chief information security officer

Knowledge about the cloud is fundamental to approaching a [policy review](./cloud-policy-review.md) with a growth mindset. The following resources can help the CISO better understand the security posture of Microsoft's Azure platform.

<!-- docutune:casing "Security Response in the Cloud" -->

**Security platform resources:**

- [Security development lifecycle, internal audits](https://www.microsoft.com/sdl)
- [Mandatory security training, background checks](https://downloads.cloudsecurityalliance.org/star/self-assessment/StandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx)
- [Penetration testing, intrusion detection, DDoS, audits, and logging](https://www.microsoft.com/security/business/operations)
- [State-of-the-art datacenter](https://azure.microsoft.com/global-infrastructure/), physical security, [secure network](/azure/security/fundamentals/network-overview)

**Privacy and controls:**

- [Manage your data all the time](https://www.microsoft.com/trust-center/privacy/data-management)
- [Control on data location](https://www.microsoft.com/trust-center/privacy/data-location)
- [Provide data access on your terms](https://www.microsoft.com/trust-center/privacy/data-access)
- [Responding to law enforcement](https://www.microsoft.com/trust-center/privacy)
- [Stringent privacy standards](https://www.microsoft.com/trust-center/privacy)

<!-- docutune:casing "Cloud Services Due Diligence Checklist" -->

**Compliance:**

- [Microsoft Trust Center](https://www.microsoft.com/trust-center)
- [Common controls hub](https://www.microsoft.com/trust-center/compliance/compliance-overview)
- [Cloud Services Due Diligence Checklist](https://www.microsoft.com/trust-center/compliance/due-diligence-checklist)
- [Regional and country compliance](https://www.microsoft.com/trust-center/compliance/regional-country-compliance)

**Transparency:**

- [How Microsoft secures customer data in Azure services](https://www.microsoft.com/trust-center)
- [How Microsoft manages data location in Azure services](https://azuredatacentermap.azurewebsites.net)
- [Who in Microsoft can access your data on what terms](https://www.microsoft.com/trust-center/privacy/data-access)
- [Review certification for Azure services, transparency hub](https://www.microsoft.com/trust-center/compliance/compliance-overview)

## Next steps

The first step to taking action in any governance strategy is a [policy review](./cloud-policy-review.md). [Policy and compliance](./index.md) could be a useful guide during your policy review.

> [!div class="nextstepaction"]
> [Prepare for a policy review](./cloud-policy-review.md)
