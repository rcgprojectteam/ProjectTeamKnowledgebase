HP DL380 Gen 9
iLO:  192.168.10.5 (Static); port 9 basement Switch (192.168.10.4)
	administrator / Q27MJFPW
MGMT: 192.168.10.6 (Static); port 10 basement Switch (192.168.10.4)
	
HyperV vSwitch - LACP Trunk; port trk1 (13,14,15) basement Switch (192.168.1.4)

LAN and vLAN:
VM-Private: Private LAN, no network connectivity
VM-Team: for VM network connectivity

VLAN 550: 
This is tagged on TRK1
DHCP on the RCG Sonicwall
Subnet: 10.5.50.0/24
Lease Scope: 10.5.50.11-10.5.50.99
DNS: 208.67.220.220, 9.9.9.9, 1.1.1.1

rcg-hvlab-dc (VM): 