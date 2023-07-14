#Scripts  _Your tags here_


```Powershell
# Script Name: CLose Open Windows
# Script Creator: Laurence Bramblett
# Date Created: 7-14-23
# Revision: 1.0
# Revision Date: 
# ~ Revision Notes ~
# - Intial Development
# Description: This will close all open windows
#-------------------------------------------------------------------------------------------------------------------------
Get-Process | Where-Object 
{$_.MainWindowTitle -ne ""} | 
ForEach-Object 
{$_.CloseMainWindow()}

```
