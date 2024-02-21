---
description: Unit 4.
---

# Manage Workspaces Across Tenants Using Azure Lighthouse

If you are required to manage multiple Microsoft Sentinel Workspaces, or workspaces which are outside your tenant, there are two options:

* Microsoft Sentinel Workspace Manager
* Azure Lighthouse

### Microsoft Sentinel Workspace Manager

This enables users to centrally manage multiple Microsoft Sentinel Workspaces within one or more Azure Tenants. The Central Workspace (with workspace manager enabled) can consolidate items to be published at scale to member workspaces. Workspace manager is enabled in configuration settings.

### Azure Lighthouse

Azure Lighthouse provides the option to enable access to the tenant, once onboarded, use the directory & subscription selector on the Azure portal to select the subscriptions containing workspaces you manage.

Lighthouse allows greater flexibility to manage resources for multiple customers without having to sign into multiple accounts/tenants.
