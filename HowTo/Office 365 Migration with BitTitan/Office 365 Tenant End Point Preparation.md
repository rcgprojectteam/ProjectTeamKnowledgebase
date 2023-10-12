## Prerequisites:
User account 'migration@domain.com' account must have long complex password as we will be creating a conditional policy to shut off MFA enforcement for the account.
Tenant must have a Microsoft Entra ID P2 license or equivalent - to be able to create conditional access policies.  


# Mailbox Impersonation

## 1. Web UI preparation - Scoped Impersonation with EWS. (Part 1)

Location: Office365/Exchange Admin Center//Recipients/Groups/Mail-enabled security.

1. Click 'Add Group'
2. Select 'Mail-enabled security' select next.
3. Give the group a reasonable name like 'impersonation', 'o365migration', or 'migration'
4. Give the group a reasonable description: Used for mail box impersonation by migration@clientdomain.com.
5. Assign 'migration@clientdomain.com' as the owner. Select Next.
6. Select next on 'add members' we will add members later with a power shell script.
7. Give the group an reasonable email address 'impersonation@clientdomain.com', 'mig@clientdomain.com', etc. Do not allow people from outside the organization to  send email to this mail-enabled security group. Do not require approval to join the group. Select Next.
8. Click Create Group.
9. Refresh the group lists then edit the group you just created.
10. Go to settings and under general settings select 'Hide this group from the global address list.' then Select Save.

## 2. PowerShell preparation - Scoped Impersonation with EWS. (Part 2)

Prerequisites: prepared mailbox list in text file, latest exchange online PowerShell module.

1. Connect to Exchange online with tenant admin creds:
```Powershell
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline
```
2. Determine if Organization Customization is turned on: (True means organizational customization hasn't been enabled yet, while false means it has been enabled.)
```
Get-OrganizationConfig | fl IsDehydrated  
```
3. If True run this command:
```
Enable-OrganizationCustomization
```
4. Retrieve the *DistinguishedName* property of the Mail Enabled Security Group created in (Part 1) by using this command wit the correct group name you chosen:
```
Get-DistributionGroup -Identity "migration" |fl name, dist*
```
Example Output:
![[migration-group.png]]
5. Copy DisginguishedName value to notepad. 
6. Create a management scope: (use DisginguishedName value copied to your note pad.)
```
New-ManagementScope "YourScopeName" -RecipientRestrictionFilter {MemberOfGroup -eq 'YourGroupDistinguisedName'}
```
Example:
![[migration-managementscope.png]]
7. Create the Management Role Assignment with this command: 
```
`New-ManagementRoleAssignment -Name "O365MigrationProject" -Role "ApplicationImpersonation" -User "migration@clientdomain.com" -CustomRecipientWriteScope "YourManagementScope"`
```
Example:
![[migration-managementrole.png]]
8. Bulk add users to the mail-enabled security group:
```
Import-Csv “C:\temp\listname.csv” | foreach{Add-DistributionGroupMember -Identity “GroupName” -Member $_.alias}
```

**TO BE UPDATED WITH EXAMPLE**

### References: 
[MigrationWiz Impersonation and Delegation for Microsoft 365 & Exchange Migrations](https://help.bittitan.com/hc/en-us/articles/115015661147-MigrationWiz-Impersonation-and-Delegation-for-Microsoft-365-Exchange-Migrations#create-a-management-scope-0-1)

# Exchange Online EWS Modern Authentication Requirements and API Configuration
	The steps listed below apply to both the source and/or destination tenant when they are Exchange Online, in regards to Exchange Web Services (EWS) in mailbox, archive mailbox, and public folder projects. Use a Global Administrator for the configuration steps.
	
	The administrator account being used for the project needs to be excluded from any MFA/2FA policies or Conditional Access policies that can block access for the administrator account. This requirement does not apply to the items or users being migrated in the project.
	
	Configuring Modern Authentication to work with MigrationWiz for mailbox, archive mailbox, and public folder projects in Exchange Online is now the default method after Microsoft discontinued support for Basic Authentication in Exchange Online after December 2022.

	The **Azure Security Defaults** must also be disabled in the tenant. (This is often enabled by default for all new Exchange Online tenants and there is **no** workaround for this requirement).

## Disable Azure Security Defaults
Location: Office365\Microsoft Entra Admin Center\Overview\

Disable Azure Security Defaults:
1. Select Overview
2. Then Select 'Properties'
3. At the bottom of the page then select 'Manage Security Defaults' a fly-out menu will appear on the right.
4. In the fly-out menu select the Security defaults drop down menu.
5. Select 'Disabled'
6. Select Save in the fly-out menu.
7. Then select Save for the Azure Active Directory properties window.
Example:
![[azureSecurityDef.png]]


## Conditional Access Policy Setup
Prerequisite: Tenant must have a Microsoft Entra ID P2 license or equivalent - to be able to create conditional access policies.  
Location: Office365\Microsoft Entra Admin Center\Protection\Conditional Access\

Conditional AccessPolicy Setup:
1. Select 'Create New Policy'
![[conditionalaccess1.png]]
2. Name the policy something relevant: 'MFA Conditional Access'
![[conditionalaccess2.png]]
3. Under Users: Include Select 'all users' under Exclude select 'Users and groups' then add your migration account to the exclude list.
![[conditionalaccess3a.png]]![[conditionalaccess3b.png]]
5. Grant: Select 'Grant Access' then select 'Require multifactor authentication.'
![[conditionalaccess4.png]]
7. Save your policy. (Policy can take 15+ minutes to populate.)
8. Verify MFA is disabled for the migration@clientdomain.com user account via the Office365 admin center and test migration account login to Office 365. 


## API Application Registration
Location: Office365\Microsoft Entra Admin Center\Applications\App Registrations\
