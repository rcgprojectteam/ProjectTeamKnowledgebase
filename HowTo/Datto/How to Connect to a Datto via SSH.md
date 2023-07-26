#knowledgebase  #Datto #SSH

# How to connect to a Datto appliance via SSH
Open your preferred SSH client and connect to partner-ssh.datto.com. You will be asked to authenticate. 
Username: partner
Password: Partner

You will then be presented a URL that you will need to log into with your Datto partner portal credentials. You copy and paste this URL into a web browser to complete your authentication.


Log in with your Datto Partner Portal login

![[Pasted image 20230726083230.png]]

Authorize the SSH access

![[Pasted image 20230726083254.png]]

You will then be connected to a scoped session with permissions to all of your available Datto Clients. As noted in the screenshot below, all sessions and inputs are recorded by Datto.

To connect to a client's Datto appliance, type connect and then the hostname of the Datto appliance. In this example I connected to a device named als-sx5

![[Pasted image 20230726083411.png]]

You can also type help to get a list of the commands that you can run. Again, note that all session information and commands are recorded, so proceed carefully.

![[Pasted image 20230726083700.png]]

Disconnect your session with a client by typing exit.  Disconnect from the relay by typing exit.
![[Pasted image 20230726083845.png]]