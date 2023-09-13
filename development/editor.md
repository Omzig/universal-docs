---
description: PowerShell Universal editor.
---

# Editor

The editor controls within the PowerShell Universal admin console provide a rich editing experience for PowerShell users. You will be able to take advantage of IntelliSense, formatting and parser error support.&#x20;

## IntelliSense

![IntelliSense](<../.gitbook/assets/image (91).png>)

All editors within PowerShell Universal will provide IntelliSense. You should be able to complete commands, parameters, built-in variables, and paths.&#x20;

There are a couple of caveats with IntelliSense.&#x20;

**IntelliSense runs within the PowerShell Universal server**

It does not rely on a configured environment to function. It runs within the PowerShell server process so will be using the current version of PowerShell 7 referenced by the server.&#x20;

**Universal Modules are Available**

Modules provided with PowerShell Universal are automatically included. You will see IntelliSense for the following modules.&#x20;

* Universal

**Modules included in PSModulePath are Available**

Any module installed into a PSModulePath will be available in IntelliSense.&#x20;

**Live Variables are Not Supported**

You will have access to built-in variables such as `ConfirmPreference` and `Host` but will not see variables specific to PowerShell Universal. &#x20;

## Formatting

![Formatting](https://blog.ironmansoftware.com/images/formatting.gif)

You can use the `Invoke-Formatter` command of `PSScriptAnalyzer` within your scripts. You will need to install `PSScriptAnalyzer` to your PSModulePath in order to use this functionality. You can format by right clicking within the editor and selecting Format or by pressing F8.&#x20;

## Syntax Errors

Syntax errors will be shown as red squiggles within the editor. Hovering over them will provide information about why the syntax error is present.&#x20;

![Syntax Errors](<../.gitbook/assets/image (427).png>)

## PSScriptAnalyzer Integration

The PowerShell Universal editor automatically integrates with PSScriptAnalyzer when it is installed on the PSU server. PSScriptAnalyzer will run against PowerShell scripts while you author them in the admin console. Warnings will be presented inline as well as an alert at the top of the editor.&#x20;

Click the alert to be navigated to the first error or warning.&#x20;

As for version 4.1, you can now specify a [PSScriptAnalyzerSettings.psd1](https://learn.microsoft.com/en-us/powershell/utility-modules/psscriptanalyzer/using-scriptanalyzer?view=ps-modules) in the root of your repository to allow for configuration of the analysis within PowerShell Universal.&#x20;
