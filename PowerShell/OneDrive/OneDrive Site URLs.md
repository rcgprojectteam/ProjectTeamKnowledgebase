#onedrive #powershell #sharepoint
# Gather OneDrive Site URL's for users:
Prerequisites: 
Tenant SharePoint admin URL: e.g. https://contoso-admin.sharepoint.com
Tenant Admin Credentials
[Latest SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588)

Run script from ISE:
```
$TenantUrl = Read-Host "Enter the SharePoint admin center URL"
$LogFile = [Environment]::GetFolderPath("Desktop") + "\OneDriveSites.log"
Connect-SPOService -Url $TenantUrl
Get-SPOSite -IncludePersonalSite $true -Limit all -Filter "Url -like '-my.sharepoint.com/personal/'" | Select -ExpandProperty Url | Out-File $LogFile -Force
Write-Host "Done! File saved as $($LogFile)."
```

## Reference:
[OneDrive URLs](https://learn.microsoft.com/en-us/sharepoint/list-onedrive-urls)