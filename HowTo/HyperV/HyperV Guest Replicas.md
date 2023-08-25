#knowledgebase  _Your tags here_

# Document Description
HyperV Guests are created with a dynamic MAC address by default. This is fine if you are not replicating the VM. If you are replacating the VM, then it is recommened to set teh MAC address to static so there are not issues with DHCP reservations or apps that require static MAC addressing

# Set up Static MAC before starting replication.
To do this, shut off the Guest OS before setting up replication. Then edit the settings, and go got Network Adapter > Advanced Featuers and select Static on the MAC address of the NIC. Repeat for each NIC. the you can enable replication

## If Virtual Machine is already replicated
If you have already enabled replication, then you will need to remove the replication. After replication is removed, then you need to clean up the replica on the destination side. Removing a VM does not remove the files, so clean that up also. And once that is done you can go to the source host and re-replicate the VM

### Header 3 Sidenotes, sub steps, or options
_If a step has multiple options, sub steps or any side notes use header 3_