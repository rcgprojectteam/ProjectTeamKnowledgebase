get-vm | ft vmname,vmid
get-vm -computername mvsc-hv1 | select-object vmid | get-vhd | ft computername,path -autosize
