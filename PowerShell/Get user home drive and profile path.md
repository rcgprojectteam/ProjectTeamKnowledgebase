#roaming #scripts #powershell #user #users
```
Get-ADUser -Filter 'enabled -eq $true' -Properties ProfilePath, HomeDirectory, HomeDrive | Select Name, SamAccountName, ProfilePath, HomeDirectory, HomeDrive | Export-Csv -path "c:\temp\userlist.csv"
```