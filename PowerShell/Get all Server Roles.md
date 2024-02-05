```
Get-WindowsFeature | Where-Object {$_.InstallState -eq 'Installed'} | Export-Csv C:\temp\roles.csv -Append -NoTypeInformation
```