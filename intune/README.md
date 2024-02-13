---
description: An introduction to Microsoft Intune, Microsoft's endpoint management service.
---

# 💾 Intune

### What is Intune?

Microsoft Intune is a cloud-based endpoint management service for both corporate and BYOD (Bring Your Own) devices.&#x20;

Intune provides a platform to manage users and devices. Intune supports BYOD (Bring Your Own Device) and devices owned solely by an organisation. Intune is what we refer to as hardware agnostic, meaning you can enrol any brand or type of device into it. For example, you can enrol Dell, Samsung, Android, Google, or Apple hardware into Intune without any issues if configured properly.

When enrolling your hardware always check that the OS version it is running is currently supported by Intune, the Microsoft documentation keeps an up-to-date list of the OS versions [Intune supports](https://learn.microsoft.com/en-us/mem/intune/fundamentals/supported-devices-browsers).

Microsoft Intune comes with an in-built app management and deployment experience. This covers app deployments, updates and removal. This will be covered further in this section. Intune also provides the Company Portal which allows users to use self-service features, like download optional apps or reset their PIN/Passwords.

Intune is integrated with Microsoft's threat defence services, including Microsoft Defender for Endpoint and other third party services. Policies can be created within Intune to respond to threats and perform real-time analysis.

### Microsoft Integrations

Intune can be used in conjunction with configuration manager to get the benefits of the web-based admin center and use Intune's cloud-based features.&#x20;

Windows Autopilot allows easy provisioning of new devices and allows those devices to be shipped directly to users. Existing devices can be re-imaged and updated to the latest Windows version. This will also be covered more in-depth in a later page.

Endpoint analytics can be configured for clear visibility and reporting on the end user experience, including device performance statistics.&#x20;

Microsoft 365 apps can be deployed directly via Intune to allow users to access the full suite of Office applications.

Microsoft Defender for Endpoint helps prevent, detect, investigate and respond to threats. A service-to-service connection be established between Defender and Intune, allowing for policies to be set up that scan files, detect threats and report back threat levels.

Windows Autopatch is an integrated cloud updating service that keeps Microsoft software current.

### Protect Data

Data can be protected on enrolled, managed devices. Intune can help isolate organisation data from personal data. On devices enrolled in Intune we can:

* Create policies that configure security settings, set password requirements or deploy certificates.
* Use mobile threat defence services to scan devices and detect threats.
* View data and reports which measure compliance.
* Control conditional access to only allow managed and compliant devices access to company resources.
* Wipe organisational data if a device is compromised or lost/stolen.

To support ta hybrid work environment, Intune allows personal device enrolment. Users have the option to enrol their devices if they want full access to organisation resources, or if they only wish to use Outlook/Teams they can take on app protection policies that enforce MFA. On devices using app management we can:

* Use threat defence services to protect app data via device scans and threat detection.
* Prevent organisation data from being copied into personal apps.
* Use app protection policies on apps and unmanaged devices.
* Restrict access to organisation email and files with conditional access.
* Remove organisational data from apps.

### Other Intune Features

Intune allows use of Windows Hello for Business instead of a password for device sign-in. WHfB lets user sign in quickly and easily. It replaces passwords with a PIN or biometric, this info is stored locally on the devices and is never sent to external devices or servers.

VPN connections can be set for remote users to allow secure access to the network. Common VPN connection partners can be used to create a VPN policy with your network settings. Within the policy you can use certificates to authenticate the connection, this lets users connect without usernames and passwords.

WiFi policy can be created within Intune which automatically connects devices to a specified SSID when within range. Certificates can be used here to authenticate the connection, eliminating the need for usernames and passwords.

Single Sign-On (SSO) can be enabled to allow users to automatically sign into apps and services using their existing Microsoft Entra organisational account.
