#knowledgebase  _Your tags #HyperV #Replication

# Document Description
HyperV Guests are created with a dynamic MAC address by default. This is fine if you are not replicating the VM. If you are replicating the VM to another host, then it is recommended to set the MAC address to static so there are not issues with DHCP reservations or apps that require static MAC addressing

# Set up Static MAC before starting replication.
To do this, shut off the Guest OS before setting up replication. Then edit the settings, and go got Network Adapter > Advanced Features and select Static on the MAC address of the NIC. This will set the NIC to keep the same MAC address it is currently using. Repeat for each NIC before you enable replication.

## If Virtual Machine is already replicated - Easy Way
The VM will still need to be powered down as above to set a Static MAC address. Once this is done run the following steps
Run the following powershell command on the source virtual host to export all the VM names and MAC addresses.
```powershell
get-vm | get-vmnetworkadapter | ft vmname, macaddress, dynamicmacaddressenabled, switchid -autosize
```
This will export a list like below:
```powershell
SQL                  00155D0A3A04
Temp-DC              00155D0A3A00
```

then on the destination host run the following powershell command
```powershell
set-vmnetworkadapter -vmname SQL -staticmacaddress 00155D0A3A04
```
## If Virtual Machine is already replicated - Hard Way
If you have already enabled replication, then you will need to remove the replication from the source. After replication is removed, then you need to clean up the replica on the destination side by deleting the VM from HyperV Manager. Also note that removing a VM does not remove the files on the destination, so clean that up also. And once that is done you can go back to the source host and re-replicate the VM.