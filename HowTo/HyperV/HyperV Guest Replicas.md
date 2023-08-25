#knowledgebase  _Your tags #HyperV #Replication

# Document Description
HyperV Guests are created with a dynamic MAC address by default. This is fine if you are not replicating the VM. If you are replicating the VM to another host, then it is recommended to set the MAC address to static so there are not issues with DHCP reservations or apps that require static MAC addressing

# Set up Static MAC before starting replication.
To do this, shut off the Guest OS before setting up replication. Then edit the settings, and go got Network Adapter > Advanced Features and select Static on the MAC address of the NIC. This will set the NIC to keep the same MAC address it is currently using. Repeat for each NIC before you enable replication.

## If Virtual Machine is already replicated
If you have already enabled replication, then you will need to remove the replication from the source. After replication is removed, then you need to clean up the replica on the destination side by deleting the VM from HyperV Manager. Also note that removing a VM does not remove the files on the destination, so clean that up also. And once that is done you can go back to the source host and re-replicate the VM.

### Header 3 Sidenotes, sub steps, or options
_If a step has multiple options, sub steps or any side notes use header 3_