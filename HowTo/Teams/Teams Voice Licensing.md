#knowledgebase  #license #office #teams #teamsvoice #voice 

# Document Description
This document covers licenses needed for Teams Voice deployment. 

### Prerequisites:
_This document assumes that the end user already has access to Teams though Microsoft Office 365 Basic/Standard or at the minimum Microsoft Teams Essentials license.

# Teams Voice - Microsoft as PSTN
_Licenses needed for Microsoft teams Voice with Microsoft as the Public Switched Telephone Network_

1. **Teams Phone with Calling Plan (country zone 1 - US) -** The Teams Phone with Calling Plan license bundles Teams Phone System's PBX capabilities and a Domestic Calling Plan for PSTN connectivity.

# Teams Voice - External PSTN (Hughes Direct Routing)
_Licenses needed for Microsoft teams Voice with an external Session Boarder Controller to Direct Routing._

1. **Microsoft Teams Phone Standard -** [Teams Phone System](https://learn.microsoft.com/en-us/microsoftteams/what-is-phone-system-in-office-365) is a hosted telephone service that gives you call control and Private Branch Exchange (PBX) capabilities. Teams Phone Standard licenses give you all Teams Phone System capabilities like cloud voicemail, caller ID, call park, call forwarding, auto attendants, call queues, call transfer, and caller ID.

# Teams Voice - Add-on and accessory licenses.
_These licenses can be used with Internal Microsoft PSTN or with an External PSTN._

1. **Microsoft Teams Shared Devices -** Many organizations require flexible workplace solutions as they shift to hybrid work scenarios. The Microsoft Teams Shared Devices license is designed to support hybrid work by allowing offices to designate devices as shared devices, including common area phones, Teams displays for hot-desks, and Teams panels for meeting spaces. For more information, see [Microsoft Teams Shared Devices licensing](https://learn.microsoft.com/en-us/microsoftteams/teams-add-on-licensing/teams-shared-device-license). This license is needed for ATA Devices to function.
2. **Communication Credits (add-on) -** Communication Credits provide a monthly pool of minutes that can be used for PSTN phone calls, if all your Calling Plan minutes get used before the beginning of the next month. If you want toll-free numbers for Audio Conferencing, auto attendants, or call queues, you'll need to [set up Communications Credits](https://learn.microsoft.com/en-us/microsoftteams/set-up-communications-credits-for-your-organization). **In order to activate the Communications credit add-on you have to add a E5 user license from the clients tenant. THIS CAN'T be a trial license!** The E5 license can be removed and credited back once the communications add-on is setup. You have a 24 hour window to do this process!
3. **Microsoft Teams Audio Conferencing with dial-out to USA/CAN -** Microsoft Teams Audio Conferencing license enables you to provide a dial-in phone number for Teams meeting attendees, and to dial-out during a meeting to invite other callers into that meeting. With Operator Connect Conferencing capabilities, organizations can use phone numbers from a third-party operator to join Microsoft Teams meetings. One Audio Conferencing license is required for each user who is going to schedule or host an audio meeting. This license is needed to meter toll free numbers along with the **Communication Credits** add-on.
4. **Microsoft Teams Phone Resource Account -**  In Microsoft Teams, all auto attendants and call queues require an associated resource account. Each resource account must be assigned a **Microsoft Teams Phone Resource Account** license to ensure they're correctly identified by the system and properly function, _regardless of whether the resource account will be assigned a telephone number_. Organizations with a subscription that includes Teams Phone are allocated a certain amount of **Teams Phone Resource Account** licenses at no extra cost. A Microsoft calling plan isn't required unless you want to be able to dial out using that resource account. For more information, see [Plan for Teams auto attendant and call queues](https://learn.microsoft.com/en-us/microsoftteams/plan-auto-attendant-call-queue#prerequisites). The **Teams Phone Resource Account** license should never be assigned to users that aren't resource accounts.


### References:
Microsoft Teams add-on licenses - https://learn.microsoft.com/en-us/microsoftteams/teams-add-on-licensing/microsoft-teams-add-on-licensing
