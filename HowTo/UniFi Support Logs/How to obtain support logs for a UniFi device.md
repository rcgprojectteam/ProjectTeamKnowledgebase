SSH into the consoles and get the logs via SSH. Here are the commands to get the support files from the UniFi Console.
 
 
ubnt-systool support /tmp/system
tar zcvf system.tar.gz /tmp/system
 
U-core logs: tar -zcvf unifi-core-logs.tar.gz /data/unifi-core/logs/
 
Protect logs:
 
 
tar -zcvf unifi-protect-logs.tar.gz /data/unifi-protect/logs/ (Without external disks)
tar -zcvf unifi-protect-logs.tar.gz /srv/unifi-protect/logs/ (With external disks)
 
 
After that, copy out the logs from Console (command construction: scp <root@Console Address>:/root/<ZIP File name> <path where you want to copy>)
NOTE: . in path means it is copied in current opened directory in the terminal.
 
 
scp root@192.168.1.1:/root/system.tar.gz .
scp root@192.168.1.1:/root/unifi-core-logs.tar.gz