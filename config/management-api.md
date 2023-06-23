# Management API

You can manage PowerShell Universal using the built in Management API. It provides the ability to perform all the actions as the admin console in an automated manner. You can view and test the API by visiting the Swagger API documentation at it's default location on your machine `http://localhost:5000/swagger/index.html` .

{% hint style="info" %}
The Management API is built in and does not require a license to Universal API.
{% endhint %}

## PowerShell Module

We provide a PowerShell module that calls the API on your behalf so you do not have to write the HTTP requests yourself. You can download this module from the PowerShell Gallery.

```powershell
Install-Module Universal
```

The PowerShell module requires an app token and computer name to call the Universal server. You can provide this items on each call.

```powershell
Invoke-PSUScript -Script $Script -ComputerName http://localhost:5000 -AppToken $AppToken
```

Additionally, you can connect to the Universal server using `Connect-UAServer`.

```powershell
Connect-PSUServer -ComputerName http://localhost:5000 -AppToken $AppToken
```

## REST API

The PowerShell Universal Management API can be accessed via REST calls. You can view the available calls using the built in Swagger API documentation. You will need an App Token to make calls to the REST API.

## App Tokens

[App Tokens](security/app-tokens.md) are required by the Management API. You will need to use an App Token with both the PowerShell Cmdlets as well as the calling the Management API directly through REST.

You can use an App Token with `Invoke-RestMethod` by specifying the authorization header.

```powershell
Invoke-RestMethod http://localhost:5000/api/v1/script -Headers @{ Authorization = "Bearer appToken" }
```
