
# The Vulnerability Details & Execution

>[!Bug]- Threat - Using Malicious Azure Apps to Infiltrate a Microsoft 365 Tenant 
><iframe width="1560" height="1015" src="https://www.varonis.com/blog/using-malicious-azure-apps-to-infiltrate-a-microsoft-365-tenant" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
>
>https://www.varonis.com/blog/using-malicious-azure-apps-to-infiltrate-a-microsoft-365-tenant
>

#  Recommended Solutions

## Number Match for Push Notifications

- Log into Microsoft Entra https://entra.microsoft.com.
- Select <font color="orange">Protection</font> on the left column.
- Then select <font color="orange">Authentication methods.</font>
- In Policies, Select <font color="orange">Microsoft Authenticator</font>
- Enable the Policy and make sure Authentication mode is set to <font color="aqua">Any</font>
- Select the Configure tab and ensure <font color="orange"> All Users</font> under Target and <font color="orange">Enabled</font> under status is selected.
- Click save

![[Number Match.gif]]

## Deny User Consent

- Log into Microsoft Entra https://entra.microsoft.com.
- Select <font color="Orange"> Identity</font>
- Then <font color="Orange"> Enterprise Applications</font>
- On the left column select <font color="Orange">Consent and permissions</font>
- Under User consent for applications select <font color="Orange">Do not allow user consent</font>.
- Under the Group owner consent select <font color="Orange">Do not allow group owner consent</font>

![[Deny User Consent.gif]]