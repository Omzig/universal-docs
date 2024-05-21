---
description: Licensing options for PowerShell Universal
---

# Licensing

PowerShell Universal is licensed per server. We provide licenses for individuals and organizations.

You can purchase a license on [our website](https://ironmansoftware.com/pricing/powershell-universal).&#x20;

## What's a server?&#x20;

A server is a single running instance of PowerShell Universal.&#x20;

### What if I have multiple containers?&#x20;

The license applies to each container instance and not the container host. For example, if you have 10 container instances running, you will need 10 licenses.&#x20;

### What if I have multiple sites on a single IIS server?

Each website running PowerShell Universal will need a license and not a single license for the entire IIS server.&#x20;

## Install a License&#x20;

To install a license, click Settings \ License. Click the Add License button to upload your license file. You can also install licenses using the `Set-PSULicense` cmdlet. Offline licenses do not require an internet connection but will need to be reinstalled when the subscription expires, in you wish to update the version of PowerShell Universal. Online licenses require an internet connection and access to `https://ironmansoftware.com` in order to verify subscription status.&#x20;

You can use the `PSULICENSE` environment variable to set a license. The value of this environment variable needs to be the contents of the license file.&#x20;

Proxy configuration can be done by clicking Settings \ General and configuring the proxy URI and, optionally, credentials. You can also configure proxy settings with the `Set-PSUSetting` cmdlet.&#x20;

## Developer Licenses

When a server license is purchased, you will be able to generate developer licenses for users building solutions for your team. Their intent is to be used by individual developers in their local environments. Do not use developer licenses when hosting a server for remote access for testing or production. Instances of PowerShell Universal running with a Developer License will display a water mark in the admin console and any apps stating they are intended only for development purposes.&#x20;

You can generate a developer license on the Settings \ License page by clicking the Generate Developer License button.&#x20;

![Generate Developer License](<.gitbook/assets/image (96).png>)

## Licensed Features

The following features of PowerShell Universal require a license.&#x20;

* Debugging Tools
* Enterprise Authentication
  * OpenID Connect
  * SAML2
  * WS-Federation
  * Windows Authentication
  * Custom Authentication Scripts
* Enterprise Authorization
  * Access Controls
  * Custom Authorization Scripts
* Git Support
* Module Management
* Non-Database Credential Vaults
* SQL Support
* Triggers
* Terminals
* Custom Login Page
* Event Hubs



