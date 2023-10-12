Prerequisites:
User account 'migration@domain.com' account must have long complex password as we will be creating a conditional policy to shut off MFA enforcement for the account.
Tenant must have a Microsoft Entra ID P2 license or equivalent - to be able to create conditional access policies.  


# Mailbox Impersonation
## Web UI preparation - Scoped Impersonation with EWS. (Part 1)
Location: Office365/Exchange Admin Center//Recipients/Groups/Mail-enabled security.
1. Click 'Add Group'
2. Select 'Mail-enabled security' select next.
3. Give the group a reasonable name like 'impersonation', 'o365migration', or 'mig'
4. Give the group a reasonable description: Use for mail box impersonation by migration@clientdomain.com.
5. Assign 'migration@clientdomain.com' as the owner. Select Next.
6. Select next on 'add members' we will add members later with a power shell script.
7. Give the group an reasonable email address 'impersonation@clientdomain.com', 'mig@clientdomain.com', etc. Do not allow people from outside the organization to  send email to this mail-enabled security group. Do not require approval to join the group. Select Next.
8. Click Create Group.
9. Refresh the group lists then edit the group you just created.
10. Go to settings and under general settings select 'Hide this group from the global address list.' then Select Save.
## PowerShell preparation - Scoped Impersonation with EWS. (Part 2)
Prerequisites: prepared mailbox list in text file, latest exchange online PowerShell module.
1. Connect to Exchange online with tenant admin creds:
```Powershell
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline
```
2. Determine if Organization Customization is turned on:
3. 