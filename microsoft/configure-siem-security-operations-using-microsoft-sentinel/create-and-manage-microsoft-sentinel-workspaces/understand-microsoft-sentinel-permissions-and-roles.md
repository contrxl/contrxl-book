# Understand Microsoft Sentinel Permissions and Roles

Microsoft Sentinel used Azure RBAC to provide built-in roles that can be assigned to users, groups and services in Azure. Azure RBAC can be used to create and assign roles within your Security Operations team to grant appropriate access to Microsoft Sentinel. Roles can be assigned in the Microsoft Sentinel Workspace directly, or in a subscription/resource group the workspace belongs to.

### Microsoft Sentinel Specific Roles

All built-in roles grant read access to the data in your workspace:

* Microsoft Sentinel Reader : can view data, incidents, workbooks, and other Microsoft Sentinel resources.
* Microsoft Sentinel Responder : all of the above, plus incident management (assign, dismiss, etc.)
* Microsoft Sentinel Contributor : all of the above, plus can edit and create workbooks, analytics rules and other Microsoft Sentinel resources.
* Microsoft Sentinel Automation Controller : allows Microsoft Sentinel to add playbooks to automation rules, not meant for user accounts.

For best results, these should be assigned to the resource group containing the Microsoft Sentinel workspace. This way, the roles apply to all the resources deployed to support Microsoft Sentinel.

### Additional Roles and Permissions

Users with certain job requirements may need other roles or specific permissions to accomplish tasks.

* Working with playbooks to automate responses to threats : playbooks are built on Azure Logic Apps and are a separate resource. Specific team members may need the ability to use Logic Apps for Security Orchestration, Automation, and Response (SOAR) operations. For this, the Logic App Contributor role can be assigned.
* Giving Microsoft Sentinel permissions to run playbooks : Sentinel uses a special service account to run incident-trigger playbooks, the use of this account increases security of the service. To grant the permissions the service account requires, your account must have Owner permissions on the resource groups containing the playbooks.
* Connecting data sources to Microsoft Sentinel : users must be assigned write permissions on the Microsoft Sentinel Workspace for this.&#x20;
* Guest users assigning incidents : if a guest user needs to assign incidents, then the user will need the Microsoft Sentinel Responder role and the user will also need the role of Directory Reader. This is a Microsoft Entra role.
* Creating and deleting workbooks : the user requires either the Microsoft Sentinel Contributer role or any lesser Microsoft Sentinel role plus the Azure Monitor role of Workbook Contributor.

### Azure Roles and Azure Monitor Log Analytics Roles

In addition to the Microsoft Sentinel dedicated roles, other Azure and Log Analytics RBAC roles can grant wider permissions.

* Azure roles grant access across all resources, including Log Analytics workspaces and Microsoft Sentinel resources:
  * Owner
  * Contributor
  * Reader
* Log Analytics roles grant access across all Log Analytics workspaces:
  * Log Analytics Contributor
  * Log Analytics Reader
