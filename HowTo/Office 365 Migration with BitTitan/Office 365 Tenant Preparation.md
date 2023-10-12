Prerequisites:
User account 'migration@domain.com' account must have long complex password as we will be creating a conditional policy to shut off MFA enforcement for the account.
Tenant must have a Microsoft Entra ID P2 license or equivalent - to be able to create conditional access policies.  


# Mail Enabled Security Group
Setup mail enabled security group to enable mailbox impersonation.
Location: Office365/Echange Admin Center//Recipients/Groups/Mail-enabled security.
1. Click 'Add Group'
2. Select 'Mail-enabled security' select next.
3. Give the group a reasonable name like 'impersonation', 'o365migration', or 'mig'
4. Give the group a reasonable description: Use for mail box impersonation by migration@clientdomain.com.
5. assign 'migration@clientdomain.com' as the owner.