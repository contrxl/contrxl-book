---
description: Unit 3.
---

# Create a Microsoft Sentinel Workspace

After designing the Workspace architecture, login to the Azure portal and search for "Sentinel", then select "Microsoft Sentinel". To enable Microsoft Sentinel, you need contributor permissions to the subscription in which the Microsoft Sentinel Workspace resides. To use Microsoft Sentinel, you need contributor or reader permissions to the resource group that the workspace belongs to.

### Create and Configure a Log Analytics Workspace

The "Add Microsoft Sentinel to a Workspace" page will display a list of available Log Analytics workspaces which Microsoft Sentinel can be added to. To create a new workspace, choose "+ create a new workspace" button. This will begin the "Create Log Analytics Workspace" process.

The "Basics" tab includes the following:

* Subscription : select the subscription.
* Resource Group : select or create a resource group.
* Name : name of the Log Analytics and Microsoft Sentinel Workspace.
* Region : location where the log data is stored.

### Add Microsoft Sentinel to the Workspace

After completing the previous steps, the "Add Microsoft Sentinel to Workspace" screen will appear. Now, wait for the newly created Log Analytics Workspace to appear and then select it and choose "Add". The new workspace is now the active screen, the Microsoft Sentinel navigation has four areas:

* General
* Threat Management
* Content Management
* Configuration

The "Overview" tab displays a standard dashboard of info about data, alerts and incidents.

### Microsoft Defender for Cloud

When creating a Microsoft Sentinel Workspace, you cannot use the Default Microsoft Defender for Cloud Log Analytics Workspace, a new Log Analytics Workspace must be created and then updated with the Microsoft Defender for Cloud tier.
