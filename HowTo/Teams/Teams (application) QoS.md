
#Scripts  #teams #qos #voice

Teams QoS is a multi-faceted project which encompasses the following:
Teams Application and the underlying client-OS
Managed Switches
Appropriate VLAN isolation for Teams-specific hardware (handsets, etc.)
QoS/CoS/DSCP marking at L3 across the client's LAN (and private WAN where implemented)
Sonicwall (or other firewall) 
Accurate knowledge of ISP-provisioned bandwidth on the DIA circuit
Accurate measurement of delivered bandwidth on the DIA circuit
Accurate knowledge of provisioned bandwidth on private 
Accurate measurement of delivered bandwidth on the DIA circuit


The following will only result in the generated traffic (by the Teams Application) have appropriate DSCP flags.  W/O implementing L3 QoS rules on switches, routers, and firewalls, this will have no impact on traffic flow.
```Powershell
#-------------------------------------------------------------------------------------------------------------------------
new-NetQosPolicy -Name "Teams Video" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50020 -IPSrcPortEndMatchCondition 50039 -DSCPAction 34 -NetworkProfile All

new-NetQosPolicy -Name "Teams Sharing" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50040 -IPSrcPortEndMatchCondition 50059 -DSCPAction 18 -NetworkProfile All

new-NetQosPolicy -Name "Teams Audio" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50000 -IPSrcPortEndMatchCondition 50019 -DSCPAction 46 -NetworkProfile All

```


<iframe width="1400" height="900" src="https://learn.microsoft.com/en-us/microsoftteams/qos-in-teams">title="Toolkit" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>




