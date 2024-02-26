---
description: Deploying files to user desktops using Intune.
---

# File Deployment

### Overview

In some situations, it can be necessary to deploy files/folders directly to user desktops. For example, run-only .exe files (like TeamViewer QS) may need to be deployed or informational PDFs/documents may need to be sent out.

To achieve this with Intune, we package the files/folder and a PowerShell script into a Win32 application and deploy it as normal.

### The Process

To see an example of this done with TeamViewer QS check [here](https://github.com/contrxl/app-gallery/tree/main/teamviewer-quick-support). You will need to download **install.cmd** and **PSscript.ps1** from that link to follow these steps. To modify the script to work with whatever files/folders are being deployed, change the following values:

* **$Folder** : change this to the exact name of the file or folder you are deploying.
* **$Destination** : change this to the directory you wish the files/folder to be deployed to, by default this is the public desktop.

Now, make sure that the **PSscript.ps1**, **install.cmd**, and the files/folder you wish to deploy are all stored in the same folder. Use the Win32 Content Prep tool to package the file into the .intunewin format. Upload this as you would with a normal Win32 application. The detection rules will need to be configured to match your deployment, select **Manually configure detection rule** and use the following:

* **Rule Type:** File
* **Path:** Set this to match the **$Destination** variable in **PSscript.ps1**
* **File or Folder:** Set this to the name of the file or folder, e.g. "File1"
* **Detection Method:** Set this to file/folder exists
* **Associated with 32-bit app on 64-bit clients:** No
