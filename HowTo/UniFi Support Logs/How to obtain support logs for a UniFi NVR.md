SSH into the consoles and get the logs via SSH.
 
```
ubnt-systool support /tmp/system
tar zcvf system.tar.gz /tmp/system
```

U-core logs: 
```
tar -zcvf unifi-core-logs.tar.gz /data/unifi-core/logs/
 ```
Protect logs:
```
tar -zcvf unifi-protect-logs.tar.gz /data/unifi-protect/logs/ (Without external disks)
tar -zcvf unifi-protect-logs.tar.gz /srv/unifi-protect/logs/ (With external disks)
``` 

After that, copy out the logs from Console (command construction: 
```
scp <root@Console Address>:/root/system.tar.gz <path where you want to copy>)
scp <root@Console Address>:/root/unifi-core-logs.tar.gz <path where you want to copy>)
```