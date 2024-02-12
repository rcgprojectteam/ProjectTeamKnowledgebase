**HP DL380 Gen 9**
Windows Server 2019 Datacenter
*As of 2/12/2024 the Connectwise agent will not install (located in c:\iso)*
"c:\\iso" has many OS install images



**iLO**:  192.168.10.5 (Static); port 9 basement Switch (192.168.10.4)
	administrator / Q27MJFPW
**MGMT**: 192.168.10.6 (Static); port 10 basement Switch (192.168.10.4)
	administrator / 1Happiness-Dumping
**HyperV vSwitch** - LACP Trunk; port trk1 (13,14,15) basement Switch (192.168.1.4)

**LAN and vLAN:**
VM-Private: Private LAN, no network connectivity
VM-Team: for VM network connectivity

**VLAN 550:** 
Tagged on TRK1
DHCP on the RCG Sonicwall; zone "LAB"; no Interface trust;
Subnet: 10.5.50.0/24
Lease Scope: 10.5.50.11-10.5.50.99
DNS: 208.67.220.220, 9.9.9.9, 1.1.1.1

**VMs:**
rcg-hvlab-dc (VM): DHCP on VLAN 550
	administrator / 1HappinessDumping
	RDP Enabled
	No roles installed
	Fully patched as of 2/12/2024