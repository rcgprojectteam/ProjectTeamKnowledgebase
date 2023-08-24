#knowledgebase #HyperV

# Error when connecting to a remote HyperV host from HyperV Manaber
If you try to add a second server in HyperV manager you may get the following error: An error occurred while attempting to connect to server (servername) Check that the Virtual Machine Management service is running and you are authorized to connect to the server

## Header 2 Step 1
[Hyper-V Manager "An error occurred while attempting to connect to server XX. Check that the Virtual Machine Management service is running and that you are authorized to connect to the server. · Issue #887 · MicrosoftDocs/Virtualization-Documentation · GitHub](https://github.com/MicrosoftDocs/Virtualization-Documentation/issues/887)

[Remotely manage Hyper-V hosts | Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/manage/remotely-manage-hyper-v-hosts)


### Header 3 Sidenotes, sub steps, or options
Check that WinRM is running on both sides. Verify they are domain joined, ping resolves correctly. Make sure the user is a member of HyperV Administrators on remote machine. Verify Firewall exceptions, or disable firewalls. If that does not work, exclude vmcompute.exe from Code Flow Guard.

1. Open "_Window Security_"
2. Open "_App & Browser control_"
3. Click "_Exploit protection settings_" at the bottom
4. Switch to "_Program settings_" tab
5. Locate "_C:\WINDOWS\System32\vmcompute.exe_" in the list and expand it
6. Click "_Edit_"
7. Scroll down to "_Code flow guard (CFG)_" and **uncheck** "_Override system settings_"
8. Start vmcompute from powershell as administrator `net start vmcompute`
9. Restart

If that does not work, set this on remote server (administrative powershell):
Enable-WSManCredSSP -Role server

Then set these on the local machine that you are running HyperV manager from (administrative powershell, obsidian is being difficult and taking out the slashes in the below example, check the MS link above or highlight it to see the slashes before locathost, client and trustedhosts):
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "fqdn-of-hyper-v-host"
Enable-WSManCredSSP -Role client -DelegateComputer "fqdn-of-hyper-v-host"

You can also try running the following, but it did not work for me. Again highlight 