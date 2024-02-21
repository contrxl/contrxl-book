---
description: Unit 2.
---

# Plan for the Microsoft Sentinel Workspace

The Microsoft Sentinel solution is installed in a Log Analytics Workspace. The most important option here is the region, as the region specifies where the log data will reside. There are three implementation options for Microsoft Sentinel:

* Single-Tenant with a single Microsoft Sentinel Workspace.
* Single-Tenant with a regional Microsoft Sentinel Workspace.
* Multi-Tenant.

### Single-Tenant Single Workspace

This Workspace will be the central repository for logs across all resources in the same tenant. This workspace receives logs from resources in other regions within the same tenant. This creates two main concerns: this can incur a bandwidth cost and there may be data governance requiring data to be kept in a specific region, meaning this isn't an option.

| Pros                                            | Cons                                       |
| ----------------------------------------------- | ------------------------------------------ |
| Central pane of glass                           | May not meet data governance requirements  |
| Consolidates all security logs and information  | Can incur bandwidth costs for cross-region |
| Easier to query all information                 |                                            |
| Azure Log Analytics RBAC to control data access |                                            |
| Microsoft Sentinel RBAC for service RBAC        |                                            |

### Single-Tenant with Regional Microsoft Sentinel Workspace

This has multiple Sentinel Workspaces which requires the creation and configuration of multiple Microsoft Sentinel and Log Analytics Workspaces.

| Pros                                                 | Cons                                                          |
| ---------------------------------------------------- | ------------------------------------------------------------- |
| No cross-region bandwidth cost                       | No central pane of glass, you can't see all data in one place |
| May be required to meet data governance requirements | Analytics, Workbooks etc. must be deployed multiple times     |
| Granular data access control                         |                                                               |
| Granular retention settings                          |                                                               |
| Split billing                                        |                                                               |

### Multi-Tenant Workspace

Multi-tenant Workspaces are used if you are required to manage a Microsoft Sentinel Workspace outside your tenant, this can be done by implementing Azure Lighthouse. This configuration grants access to the tenants.

The same Workspace should be used for both Microsoft Sentinel and Microsoft Defender for Cloud, to ensure all logs collected by Defender can also be used by Microsoft Sentinel.
