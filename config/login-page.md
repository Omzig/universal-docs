---
description: Documentation on how to customize the login page.
---

# Login Page

{% hint style="info" %}
Login page customization requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

The login page colors, image, copyright and title can be customized by editing the `.universal/loginPage.ps1` file.

## Customizing the login page

You can host an image by using [Published Folders](../platform/published-folders.md). In this example, we have a `dbatools.png` file in our local folder.

![DBATools Logo](<../.gitbook/assets/image (401).png>)

Next, we can create a `loginPage.ps1` file in the repository folder. Add the various colors, text and image URL to customize the login page. As soon as you save this file, you can refresh the login page to see the result.

```powershell
$LoginPage = @{
 PrimaryColor = '#5c2751' 
 Title = 'DBATools Web Portal'
 Copyright = 'DBATools 2020' 
 HeaderFontColor = 'white'
 HeaderColor = '#4bc0d9' 
 SecondaryColor = '#6457a6'
 SecondaryFontColor = 'white'
 Image = 'http://localhost:5000/images/dbatools.png'
 Links = @(
    New-PSULoginPageLink -Text 'Google' -Url 'http://www.google.com'
    New-PSULoginPageLink -Text 'Microsoft' -Url 'http://www.microsoft.com'
 )
}

New-PSULoginPage @LoginPage
```

This login page looks like this.

![](<../.gitbook/assets/image (71).png>)

## Customizing the login page in the Admin Console

{% hint style="warning" %}
This feature will be available in PowerShell Universal 2.3.&#x20;
{% endhint %}

In addition to being able to customize the login page via PowerShell, you can also do so in the admin console. Click Settings \ Login page to adjust the settings.&#x20;

![](<../.gitbook/assets/image (515).png>)

## Customizing the login page with a Dashboard

You can override the login page with a dashboard by setting a dashboard's base URL to `/login`. You need to ensure that the dashboard does not require authentication.&#x20;

```powershell
New-PSUDashboard -Name 'Dashboard' -Path 'dashboard.ps1' -BaseUrl '/login'
```

You will then need to implement the login features manually.&#x20;

## API

* [New-PSULoginPage](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSULoginPage.txt)
* [New-PSULoginPageLink](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSULoginPageLink.txt)

###
