This is not a simple copy-pasta.  Read and understand what you're doing and why:
===========
config
hostname <client-switch>
ip dns server-address priority 1 208.67.220.220
ip dns server-address priority 2 208.67.222.222
time daylight-time-rule continental-us-and-canada
time timezone -360
ntp server-name 0.pool.ntp.org iburst
ntp server-name 1.pool.ntp.org iburst
ntp server-name 2.pool.ntp.org iburst
timesync ntp
ntp unicast
ntp enable
spanning-tree log state-transitions instance cst
spanning-tree log state-transitions vlan 1
spanning-tree
loop-protect <port-range> receiver-action send-disable
loop-protect transmit-interval 10
loop-protect disable-timer 600
logging origin-id hostname
logging notify running-config-change transmission-interval 1
logging 52.27.103.243
no aruba-central enable
snmp-server community "<communityName>" operator restricted
snmp-server contact "RCG - 309-762-3589"
snmp-server location "<location at client>"
crypto key generate ssh  
ip ssh 
no ip ssh cipher aes128-cbc 
no ip ssh cipher 3des-cbc 
no ip ssh cipher aes192-cbc 
no ip ssh cipher aes256-cbc 
no ip ssh cipher rijndael-cbc@lysator.liu.se 
no ip ssh cipher aes128-ctr 
no ip ssh cipher aes192-ctr 
no ip ssh mac hmac-md5 
no ip ssh mac hmac-sha1-96 
no ip ssh mac hmac-md5-96 
lldp run
lldp config all medTlvEnable network_policy
lldp config all medTlvEnable capabilities
banner motd * 
This system is for authorized use only. Unauthorized or improper 
use of this system may result in civil or criminal penalties. By 
continuing to use this system you acknowledge your consent to 
these conditions of use. 
* 
no snmp-server community "public"
interface vlan 1
  name "Default_VLAN"
  ip address dhcp-bootp
  untagged 1-48
  qos priority 2
  exit
interface vlan 600
   name "NVR-Security Cams"
   tagged 1-48
   qos priority 1
   exit
interface vlan 500
   name "Guest WiFi"
   tagged 1-48
   qos priority 0
   exit
interface vlan 1031
   name "Management"
   tagged 1-48
   qos priority 6
   exit
interface vlan 2318
   name "VoIP Phones"
   tagged 1-48
   qos dscp ef
   exit
write memory 

=======
**Note:  In order for the remote syslog to work, we must update the syslog configuration on our syslog collector.  As of 9/2023 this lives at the AWS server known as 'dewey'**
=======

Other Commands
===========
management-vlan 1031
copy tftp flash <TFTP-IP> <filename> secondary
boot system flash secondary
copy flash flash primary
trunk <port-list> <trk1 ... trk144> <trunk | lacp>
erase startup-configuration
copy tftp pub-key-file <tftp-IP> pubKEY.txt manager
ip ssh public-key manager 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDjxU082A/MUo1CT7o5DSCT9sfSVLrfvMYYF8S25Ran0UVNlQN0skDgR3Z9VSQC+z771hebbMfC8EFMh4C3AxqFdlCudnwW4yv9xvu8sNGE3b+KqPDNVhT/rVcPPoAsxWm6ycZsNWfL621Vbpb47y+y8T2sgxSjpfXYtTMN44Eo5GF5BEj5SP6Yolj071eYmrg4AnM+OcVy5IwGt5wqGZbbs2mcOxnEPNmSCB++zlbYZ1He2UmIYymspXPOqZEWjyLpK7bDJqflR1IvZneDMxFVUIXThbHoE12bJfykguzGBqSLcRe6zQQz08olqD+u4RAgaNgAd8nvp8MXReCe7inR tlsPrivate' username manager
aaa authentication ssh login public-key 
aaa authentication ssh enable tacacs local
clear crypto client-public-key
include-credentials

ip dns server-address priority 1 8.8.8.8 oobm
ip dns server-address priority 2 1.1.1.1 oobm

Initial authentication config:
aaa authentication ssh login local
aaa authentication ssh enable local

Set passwords for manager, do not set password for operator.
password manager

copy tftp pub-key-file 10.0.30.2 pubKey.txt operator <oobm>

turn on pki for operator with no secondary auth:
aaa authentication ssh login public-key none

interface 45
   monitor
   exit
mirror 1 port 37

Set DHCP Server with static binding
============
vlan 2318
    name "DHCP_VoIP_VLAN"
    ip address 10.23.18.3 255.255.255.0
    dhcp-server
exit
dhcp-server pool "IoT Mgmt"
     authoritative
     default-router "10.23.18.1"
     dns-server "208.67.220.220,208.67.222.222"
     domain-name "mclbody.com"
     network 10.23.18.0 255.255.255.0
     range 10.23.18.11 10.23.18.99
	 lease 00:23:59
	 static-bind ip 10.1.1.254 255.255.255.255 mac aa:bb:cc:dd:ee:ff
exit
dhcp-server enable

aaa port-access local-mac profile "yealinkProfile"
   vlan tagged 2318
   cos 5
   exit
aaa port-access local-mac mac-group "yealinkGroup" mac-oui 805E0C
aaa port-access local-mac apply profile yealinkProfile mac-group yealinkGroup
aaa port-access local-mac  1-12
aaa authentication allow-vlan tagged

dhcp-snooping authorized-server 192.168.1.20
dhcp-snooping vlan 1
interface trk1
   dhcp-snooping trust
   exit
dhcp-snooping

hostname "SWITCH-NAME"
radius-server host 18.204.0.31
radius-server host 54.203.27.225
radius-server dead-time 5
radius-server key "<SECRET-KEY>"
radius-server retransmit 2
aaa authentication num-attempts 8
aaa authentication ssh login radius
aaa authentication ssh enable radius

 spanning-tree mode mstp 
   spanning-tree config-name reg
   spanning-tree config-revision 1
   spanning-tree inst 1 vlan 1 32 510 1032
   spanning-tree inst 2 vlan 30 253
   spanning-tree
   
   show spanning-tree
   
   spanning-tree bdpu-filter
   spanning-tree cost
   spanning-tree instance cost

============
Other Notes
============
HP 1920 '_cmdline-mode on' then Jinhua1920
unauthorized
HP 1950 xtd-cli-mode password: foes-bent-pile-atom-ship

UniFi SW: 0x01;0x04;0x34;0xA5;0xEB;0x1D

https://ine.com/blog/2010-02-22-understanding-mstp#CAVEATS
https://techhub.hpe.com/eginfolib/networking/docs/switches/WB/15-18/5998-8156_wb_2926_atmg/content/ch03s07.html

