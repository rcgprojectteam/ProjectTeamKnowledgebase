#knowledgebase  #teams #ATA #FAX #POTS #Analog #Phone

# Onboarding Cisco Analog Telephone Adapter 190 Series Device.
An analog telephone adapter (ATA) is a device for connecting traditional analog devices to a digital telephone system. In context of (SIP) Session Initiation Protocol (GW) Gate Way, it connects these analog devices via SIP GW to Microsoft Teams.

### Pre-Requisites:
1. Licenses: **Microsoft Teams Shared Devices** and **Teams Phone with Calling Plan (country zone 1 - US)**
2. Assignable DID number.
3. Cisco ATA192-MPP Device

# Office 365 User Configuration
1. Log into Office 365 tenant.
2. Create a new user, if the ATA deice is used for faxing name the account 'fax@clientname.com' Document password in ITGlue and MFA the account.  Use TOTP auth from ITGlue. Enforce MFA.
3. Assign 'Microsoft Teams Shared Devices' and 'Teams Phone with Calling Plan (country zone 1 - US)' licenses to the user account.
4. Open the (TAC) Teams Administration Center
5. Go to Voice/Phone Numbers.
6. Select a number and click on Edit.
7. Assign number to the fax@companymane.com account.

# Office 365 Tenant Configuration
## Configure Teams Voice for ATA SIP Device.

In O365/TAC/Voice/Calling Policies
1. Add a new calling policy - "Allow SIP calling".
2. Edit New Teams calling policy - Turn on setting "SIP Devices can be used for calls."
3. Make sure your Calling Policy allows SIP devices to be used for calls (slider right near the bottom)
4. Save the new policy.
5. Select the new calling policy.
6. Select 'manage users/assign users'
7. Add the fax user and then select apply.

# Provision and enroll Cisco ATA SIP Device.
## Provision the Cisco ATA192 hardware.
1. Get the latest firmware from cisco for the Cisco ATA.
2. Install the latest firmware: Administrator ->Firmware Upgrade
3. Reboot.
4. Reset Admin Password: Administration -> Management -> User List 
5. Select edit button for Admin user. 
6. Create a complex password and store it in ITGlue for the client. 'User - Cisco ATA192 - Admin'
7. Enable Remote Management: Administration -> Management ->  Web Access Management. Select 'Enabled' on the Remote Management selection. Enable HTTPS.
9. Assign Profile Provisioning Rule: Voice -> Provisioning -> Profile Rule
10. Enter this URL: `http://noam.ipp.sdg.teams.microsoft.com/mac.cfg`
11.  Save Configuration, the ATA will reboot.
##  Pair Cisco ATA192 in Office 365
1. From TEC navigate to Teams Devices -> SIP Devices -> Actions -> Provision Devices
2. Select 'Add MAC addresses manually'
3.  

### In Process stuff below:
- Provision and enroll SIP devices as common area phones. [Here.](https://learn.microsoft.com/en-us/microsoftteams/sip-gateway-configure#provision-and-enroll-sip-devices-as-common-area-phones)

In Powershell: (to be reviewed further, might not need this step.)
- IP Phone Policy where the sign in mode is set to CommonAreaPhoneSignIn (you have to do this through PowerShell, its not visible in the Admin Centre)
- This assumes you have the Teams Administration Powershell Module installed, if not click [here.](https://www.powershellgallery.com/packages/MicrosoftTeams/5.4.0)
- You also need an active Teams Shared Device license in the tenant.
```
Import-Module MicrosoftTeams
Connect-MicrosoftTeams
Set-CsTeamsIPPhonePolicy -Identity CommonAreaPhone -SignInMode CommonAreaPhoneSignin
```
In O365 Tenant:
- Make sure your user account has an Shared Device License.
- Make sure your user account has a PSTN number assigned (Use a Calling Plan)
- SIP Gateway provisioning server URL - > Americas: `http://noam.ipp.sdg.teams.microsoft.com`

- Microsoft SIP Gateway pairing portal - https://portal.sdg.teams.microsoft.com/

## Licenses Needed:
- Microsoft Teams Shared Devices - Enables the use of non-Teams Rooms shared devices with Microsoft Teams - From ‎$8.00‎ ‎licenses‎/month
- Microsoft Teams Phone with Calling Plan‎ - ‎Teams Phone with Calling Plan (country zone 1 - US)‎ - For users in the United States and Puerto Rico. - From ‎$12.00‎ ‎licenses‎/month



### References

1. Configure SIP Gateway - https://learn.microsoft.com/en-us/microsoftteams/sip-gateway-configure
2. Cisco ATA 191 and 192 Analog Telephone Adapter Multiplatform Phones Release Notes for Firmware Release 11.1(0) - https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cata/19x/3PCC/firmware/11-1-1/release_notes/at92_b_cisco-ata-191-and-192.html#task_D84DAFD51D92A2AADCCBAE3643F21DCD
3. Cisco Forum Setup Thread - https://community.cisco.com/t5/webex-devices/cisco-ata-191-microsoft-teams-sip/m-p/4761129
4. Cisco ATA 192 Multiplatform Analog Telephone Adapter, 2-Port Handset-to-Ethernet Adapter, 1-Year Limited Hardware Warranty (ATA192-3PW-K9) - https://www.amazon.com/Cisco-2-Port-Telephone-Adapter-Multiplatform/dp/B07BTSK3SS
5. GitHub - SIP Gateway Analog Docs - https://github.com/darylhunter/SIPGatewayAnalogDocs/blob/main/Onboarding%20Cisco%20ATA%2019x%20with%20Microsoft%20SIP%20Gateway%20v10.31.22.pdf
6. Microsoft Teams IP Phone Policy -  https://learn.microsoft.com/en-us/powershell/module/skype/set-csteamsipphonepolicy?view=skype-ps
7. Provision and enroll SIP devices as common area phones - https://learn.microsoft.com/en-us/microsoftteams/sip-gateway-configure#provision-and-enroll-sip-devices-as-common-area-phones
8. Microsoft - Setup Common Area Phones - https://learn.microsoft.com/en-us/microsoftteams/set-up-common-area-phones
