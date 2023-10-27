Presumes that the UPN list includes the new domain suffix
# Edit below as appropriate to the client

$newDomain1 = "empoweringabilities.org"
#$newDomain2 = "empoweringabilitiesqc.org"
$smtp = "smtp:"

$users = Get-ADUser -Filter * -SearchBase "OU=365 Sync,DC=hdcnet,DC=Local" -Properties *

forEach ($user in $users) {
   $prefix, $domain = $user.UserPrincipalName.split("@")
   $newProxy1 = $smtp + $prefix + "@" + $newDomain1
   #$newProxy2 = $smtp + $prefix + "@" + $newDomain2

   $user.ProxyAddresses += $newProxy1
   #$user.ProxyAddresses += $newProxy2
   write-Host $user.Name, ",", $user.UserPrincipalName,",","+ProxyAddresses: ", $newProxy1
    
   Set-ADUser -Instance $User
}