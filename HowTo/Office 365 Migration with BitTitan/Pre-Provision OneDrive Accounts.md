#onedrive #o365 #Scripts #powershell


csv template:
```
user1@contoso.com
user2@contoso.com
user3@contoso.com
```

Powershell Syntax: 
```
$users = Get-Content -path "C:\temp\users.txt" Request-SPOPersonalSite -UserEmails $users
```

##References:
[Office 365 - Pre-Provision Accounts](https://learn.microsoft.com/en-us/sharepoint/pre-provision-accounts)
