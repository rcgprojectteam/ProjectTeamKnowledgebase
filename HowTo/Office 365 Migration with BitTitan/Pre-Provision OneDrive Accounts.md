#onedrive #o365 #Scripts #powershell


CSV Template:
```
user1@contoso.com
user2@contoso.com
user3@contoso.com
```

Powershell Syntax: 
```
Connect-SPOService -Url https://contoso-admin.sharepoint.com
$users = Get-Content -path "C:\temp\users.csv" Request-SPOPersonalSite -UserEmails $users
```

##References:
[Office 365 - Pre-Provision Accounts](https://learn.microsoft.com/en-us/sharepoint/pre-provision-accounts)
