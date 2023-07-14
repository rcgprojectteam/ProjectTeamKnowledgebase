#knowledgebase  #teams #ATA #FAX #POTS #Analog #Phone

# Onboarding Cisco Analog Telephone Adapter 190 Series Device.
An analog telephone adapter (ATA) is a device for connecting traditional analog devices to a digital telephone system. In context of (SIP) Session Initiation Protocol (GW) Gate Way, it connects these analog devices via SIP GW to Microsoft Teams.

# Header 1
_A brief description on what the first goal is and/or information. **Make sure the text hugs the header in this format**_ 

## Office 365 Tenant Configuration
### Configure Teams Voice
In O365/TAC/Voice/Calling Policies
1. Add a new calling policy - "Allow SIP calling".
2. Edit New Teams calling policy - Turn on setting "SIP Devices can be used for calls."
3. 

- Make sure your Calling Policy allows SIP devices to be used for calls (slider right near the bottom)
- Make sure your user account has an Shared Device License, and [IP Phone Policy](https://learn.microsoft.com/en-us/powershell/module/skype/set-csteamsipphonepolicy?view=skype-ps) where the sign in mode is set to CommonAreaPhoneSignIn (you have to do this through PowerShell, its not visible in the Admin Centre)
- Make sure your user account has a PSTN number assigned (We used a Calling Plan number which worked fine)

Microsoft Teams Shared Devices - Enables the use of non-Teams Rooms shared devices with Microsoft Teams -From ‎$8.00‎ ‎licenses‎/month

### References

1. Configure SIP Gateway - https://learn.microsoft.com/en-us/microsoftteams/sip-gateway-configure
2. Cisco ATA 191 and 192 Analog Telephone Adapter Multiplatform Phones Release Notes for Firmware Release 11.1(0) - https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cata/19x/3PCC/firmware/11-1-1/release_notes/at92_b_cisco-ata-191-and-192.html#task_D84DAFD51D92A2AADCCBAE3643F21DCD
3. Cisco Forum Setup Thread - https://community.cisco.com/t5/webex-devices/cisco-ata-191-microsoft-teams-sip/m-p/4761129
4. Cisco ATA 192 Multiplatform Analog Telephone Adapter, 2-Port Handset-to-Ethernet Adapter, 1-Year Limited Hardware Warranty (ATA192-3PW-K9) - https://www.amazon.com/Cisco-2-Port-Telephone-Adapter-Multiplatform/dp/B07BTSK3SS
5. GitHub - SIP Gateway Analog Docs - https://github.com/darylhunter/SIPGatewayAnalogDocs/blob/main/Onboarding%20Cisco%20ATA%2019x%20with%20Microsoft%20SIP%20Gateway%20v10.31.22.pdf