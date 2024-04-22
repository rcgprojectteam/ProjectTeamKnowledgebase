```
Get-ADComputer -Filter 'enabled -eq "true"' `
-Properties Name,Operatingsystem,OperatingSystemVersion,IPv4Address |
Sort-Object -Property Operatingsystem |
Select-Object -Property Name,Operatingsystem,OperatingSystemVersion,IPv4Address |  Export-Csv C:\temp\workstations.csv -Append -NoTypeInformation
```

```
Get-ADcomputer -Filter * -properties * | Select Name, OperatingSystem, Lastlogondate  |  Export-Csv C:\temp\workstations.csv -Append -NoTypeInformation
```