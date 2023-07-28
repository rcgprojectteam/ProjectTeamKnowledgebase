#Scripts  _Your tags here_


```Powershell
# Script Name: Display Hardware Information
# Script Creator: Laurence Bramblett
# Date Created: 7/14/23
# Revision: 1.0
# Revision Date: 
# ~ Revision Notes ~
# - Intial Development
# Description: Used to get hardware information
#-------------------------------------------------------------------------------------------------------------------------
# - Hard Drive Information

wmic diskdrive get model,serialnumber

# - CPU Information

wmic cpu get name

# - All System Information

systeminfo
```
