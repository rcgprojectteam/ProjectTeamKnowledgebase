#Scripts  _Your tags here_


```Powershell
# Script Name: List Installed Features on a Server
# Script Creator: Laurence Bramblett
# Date Created: 7/14/23
# Revision: 1.0
# Revision Date: 
# ~ Revision Notes ~
# - Intial Development
# Description: Lists Instaled Features on a Server
#-------------------------------------------------------------------------------------------------------------------------

Get-WindowsFeature | Where-Object {$_.Installed -eq "True"} | Select-Object -Property DisplayName

# - 
```
