
Connect to Entra Active Directory
```
Connect-MsolService
```

Check Directory Sync Status
```
Get-MsolDirSyncConfiguration
```

Disable Directory Sync
```
Set-MsolDirSyncEnabled -EnableDirsync $False
```
