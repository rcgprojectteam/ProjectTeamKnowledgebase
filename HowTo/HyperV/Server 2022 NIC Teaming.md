#knowledgebase  #HyperV #NICTeaming

# Server 2022 NIC Teaming 
Using a LBFO NIC team in Server 2022 for HyperV has been depricated. The new model is to use a SET NIC Team, which per MS documentation is recommended for 10 GB links and above, and all hardware and driver versions must be the same

# How to create a HyperV virtual switch using a LBFO Team
[Bypass LBFO Teaming deprecation on Hyper-V and Windows Server 2022 - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/windows-server-for-it-pro/bypass-lbfo-teaming-deprecation-on-hyper-v-and-windows-server/m-p/3672310)
New-VMSwitch -Name "VM Traffic" -NetAdapterName "VM Traffic Team" -AllowNetLbfoTeams $true -AllowManagementOS $false

## SET Information
_Initial description of or information regarding step1_

### Header 3 Sidenotes, sub steps, or options
_If a step has multiple options, sub steps or any side notes use header 3_