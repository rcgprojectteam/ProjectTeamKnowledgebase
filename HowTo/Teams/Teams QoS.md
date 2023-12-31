
#Scripts  #teams #qos #voice

##  Teams QoS is a multi-faceted project which encompasses the following:

> - Teams Application and the underlying client-OS - set appropriate DSCP marks
> - Appropriate VLAN isolation for Teams-specific hardware (handsets, etc.)
> - QoS/CoS/DSCP marking at L3 across the client's LAN (and private WAN where implemented)
> - Sonicwall (or other firewall) bandwidth management configuration

### Pre-requisite information before ANY QoS implementation:

> - Accurate knowledge of ISP-provisioned bandwidth on the DIA circuit
>> -  Accurate measurement of delivered bandwidth on the DIA circuit
> - Accurate knowledge of provisioned bandwidth on private WAN circuits
>>  - Accurate measurement of delivered bandwidth on private WAN circuits

### ***Ongoing management and communication with the client when provisioned rates on WAN links (including DIA) are changed***

### <span style="color:red">Note that as a general rule QoS matters most at the upstream link when that link is significantly smaller then the downstream links feeding traffic into the upstream link. </span> 


## Network Switch configuration for VoIP Hardware

#### HPE/Aruba VLAN packet marking is accomplished using the following within the VLAN context:
> - qos dscp ef

#### UniFi Switches (not Ubiquiti EdgeSwitches)
> - No real ability to specifically and selectively mark traffic

## Sonicwall Bandwidth Management 
This creates rules to trigger on Teams Voice Softphone traffic.  Prioritizing handsets would require another access rule+BW shaping using zones VoIP -> WAN

Overview:
Create Service objects as follows:

![[Pasted image 20230717100533.png]]

Create Service Groups as follows:

![[Pasted image 20230717100639.png]]

Create Bandwidth Profile Objects as follows:
> - The values of Guaranteed and Maximum can be adjusted.  
> - '**guaranteed**' sort-of reserves that amount away from the available bandwidth on the interface.
> - '**maximum**' allows the prioritization to influence flow up to this value.  Usage over that value is handled w/o shaping.


![[Pasted image 20230717100755.png]]

Update the WAN interface(s) with appropriate BW Management values as follows:
> - The example below is for a 100Mbps symmetric service

![[Pasted image 20230717100929.png]]

Create an access rule as follows:

![[Pasted image 20230717101149.png]]

![[Pasted image 20230717101239.png]]

![[Pasted image 20230717101255.png]]


You can monitor if the rule is triggering by viewing the following page on the firewall:

![[Pasted image 20230717101427.png]]


Fundamental Bandwidth HowTo:
<iframe width="1400" height="900" src="https://www.sonicwall.com/support/knowledge-base/how-can-i-configure-bandwidth-management/170521130013462/">title="Toolkit" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Teams Application packet marking
The following will only result in the generated traffic (by the Teams Application) having appropriate DSCP flags.  W/O implementing QoS rules on switches, routers, and firewalls, this will have no impact on traffic flow.
```Powershell
#-------------------------------------------------------------------------------------------------------------------------
new-NetQosPolicy -Name "Teams Video" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50020 -IPSrcPortEndMatchCondition 50039 -DSCPAction 34 -NetworkProfile All

new-NetQosPolicy -Name "Teams Sharing" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50040 -IPSrcPortEndMatchCondition 50059 -DSCPAction 18 -NetworkProfile All

new-NetQosPolicy -Name "Teams Audio" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50000 -IPSrcPortEndMatchCondition 50019 -DSCPAction 46 -NetworkProfile All

```

```Registry Keys:
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\QoS]

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\QoS\Teams Sharing]
"Version"="1.0"
"Application Name"="teams.exe"
"Protocol"="*"
"Local Port"="50040:50059"
"Local IP"="*"
"Local IP Prefix Length"="*"
"Remote Port"="*"
"Remote IP"="*"
"Remote IP Prefix Length"="*"
"DSCP Value"="18"
"Throttle Rate"="-1"

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\QoS\Teams Video QoS]
"Version"="1.0"
"Application Name"="teams.exe"
"Protocol"="*"
"Local Port"="50020:50039"
"Local IP"="*"
"Local IP Prefix Length"="*"
"Remote Port"="*"
"Remote IP"="*"
"Remote IP Prefix Length"="*"
"DSCP Value"="34"
"Throttle Rate"="-1"

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\QoS\Teams Voice QoS]
"Version"="1.0"
"Application Name"="teams.exe"
"Protocol"="*"
"Local Port"="50000:50019"
"Local IP"="*"
"Local IP Prefix Length"="*"
"Remote Port"="*"
"Remote IP"="*"
"Remote IP Prefix Length"="*"
"DSCP Value"="46"
"Throttle Rate"="-1"
```
<iframe width="1400" height="900" src="https://learn.microsoft.com/en-us/microsoftteams/qos-in-teams">title="Toolkit" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>




