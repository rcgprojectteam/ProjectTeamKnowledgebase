#roaming #scripts #powershell #user #users
```
Get-ADUser -Filter 'enabled -eq $true' -Properties ProfilePath, HomeDirectory, HomeDrive, ScriptPath | Select Name, SamAccountName, ProfilePath, HomeDirectory, HomeDrive, ScriptPath | Export-Csv -path "c:\temp\userlist.csv"
```