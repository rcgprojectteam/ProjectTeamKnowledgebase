#Scripts  _Your tags here_


```Powershell
# Script Name: List Installed Applications
# Script Creator: Laurence Bramblett
# Date Created: 7/14/20
# Revision: 1.0
# Revision Date: 
# ~ Revision Notes ~
# - Intial Development
# Description: List Installed Applications
#-------------------------------------------------------------------------------------------------------------------------
wmic product get name,version

# - Export to CSV

wmic product get name,version /format:csv > installed_apps.csv

# - This exports to C:\Users\USERNAME

```
