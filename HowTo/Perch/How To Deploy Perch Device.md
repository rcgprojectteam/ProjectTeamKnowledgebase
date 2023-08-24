#Knowledgebase #HowTo #Perch #Technologies 

# Document Description
This document covers the process and steps to deploying a Perch device at a client. This includes notes from the 30-minute Pre-Install phone call, installation instructions, Onboarding, and the first alert review.

> [!info]- Scoping a Physical Perch Device
> ![[ConnectWise SIEM Sensor Scoping_Jun 2022 (2) 1.pdf]]
> 

> [!Info]- Perch Pricing for Physical Sensor
> ![[CW_SIEM_Q2_2023_Sensor_Pricing.pdf]]
> 

# Getting started
You will receive a few e-mails after an agreement has been made with the client. The information and examples are contained below.

## Phases of Deployment
Phase 1: Pre-Install – 30 minutes.
Phase 2: Installation – 1.5 hours.
Phase 3: Onboarding – 1 hour.
Phase 4: The 1st Alert Review – 30 minutes.

## Support Contacts
[securityonboarding@connectwise.com](mailto:securityonboarding@connectwise.com)
- Perch account status, upcoming/ongoing deployments, and onboarding questions.

[Perch.help@connectwise.com](mailto:Perch.help@connectwise.com)
- Integrations, event notifications, Sensor or SIEM issues or any request for technical assistance.

[Securitypartnersupport@connectwise.com](mailto:Securitypartnersupport@connectwise.com)
- E-mail address used for ConnectWise Security Support.

## Support Portal Registration & Ticket Access
You will need to login and/or create an account to maintain the deployment ticket for Perch. This is where all the details of the deployment will be including but not limited to your assigned ConnectWise engineer.

- Go to: [https://support.carvir.net/support/login](https://support.carvir.net/support/login)
- If you don’t have an account, you will need to sign up for one.
- Select the Tickets tab in the green navigation bar (left hand corner).
- Change filter to All Tickets.
- Select the project ticket.

# Virtual Perch Sensor Deployment
Virtual sensor is usually Rouse’s go-to solution. It’s easier to maintain, deploy, setup, and its cheaper. Since this is the installation type we lean towards, we will focus on this first.

Please Note: _Hyper-V 2016 does not work with most Broadcom/QLogic network cards. To determine if it would be supported in your environment, please follow the steps listed below. Once you have saved your new virtual switch, open Virtual Switch manager again. Expand your new virtual switch and select Extensions. If the NDIS capture box is still checked, your install will be supported. If the box is now unchecked your Broadcom/Qlogic cards are not supported._

## Minimum Requirements
- 12GB RAM
- 256GB for vHDD
- 4 Virtual Cores
- Verify there is an available Physical NIC in Network Connections. (2 preferred Mgmt/Monitor).

## Sensor Downloads
- Hyper-V Sensor: [https://bit.ly/perch-hyperv](https://bit.ly/perch-hyperv)
- VMware Sensor: [https://bit.ly/perch-ova](https://bit.ly/perch-ova)
- Log Shipper: [https://cdn.perchsecurity.com/downloads/perch-log-shipper-latest.exe](https://cdn.perchsecurity.com/downloads/perch-log-shipper-latest.exe)

## Hyper-V Port Mirroring
Identify an open physical NIC on the Hyper-V host to connect to the mirror port you have configured in the switch. If you have a switch capable of RSPAN, you can leverage that instead of a dedicated physical NIC. You can view the adapters in Network Connections within the Control Pane.

1. Open the Hyper-V manager and connect to the desired Hyper-V host to manage
2. In the right pane, choose Virtual Switch Manager
3. Create a new External switch by choosing External and clicking Create New Virtual Switch
4. Name the switch appropriately (e.g. Mirror_Switch)
5. Choose the same physical NIC you identified previously and designate it as the external NIC to connect to then choose OK
6. Open a PowerShell session on the Hyper-V host and execute the following commands:

```Powershell
$a = Get-VMSystemSwitchExtensionPortFeature -FeatureId 776e0ba7-94a1-41c8-8f28-951f524251b5
```

```Powershell
$a.SettingData.MonitorMode = 2
```

```Powershell
add-VMSwitchExtensionPortFeature -ExternalPort -SwitchName Mirror_Switch -VMSwitchExtensionFeature $a
```

```Powershell
Get-VMNetworkAdapter -VMName "NAME OF THE PERCH SENSOR"
```
<font color="Orange"> *If the MAC address's come up as 000000000000, you will need to assign the NIC's and start the VM first. </font>

```Powershell
Get-VMNetworkAdapter -VMName "NAME OF THE PERCH SENSOR" | Where-Object -Property MacAddress -eq "MONITOR MAC HERE" | Set-VMNetworkAdapterVlan -Trunk -AllowedVlanIdList "0-4064" -NativeVlanId "0"
```
_Please note: These commands will enable the virtual switch to receive packets from the physical mirror port._

7. In the right pane of Hyper-V manager, choose Virtual Switch Manager again
8. Select the newly created Mirror_Switch
9. Expand the Virtual Switch by selecting the + next to the switch name
10. Choose Extensions
11. Ensure Microsoft NDIS Capture is a selected extension
12. Click **OK** to apply the settings and exit the Virtual Switch Manager.

## Importing A Hyper-V Virtual Sensor
If you haven’t done so already, please setup [Hyper-V Port Mirroring](#_Hyper-V_Port_Mirroring) first. Then initiate the download for the virtual sensor from the links in the [Sensor Downloads](#_Sensor_Downloads) section of this document. _Please note that the download will occur immediately, so before assuming the link is broken check the downloads in your browser. The actual webpage you will be brought to is blank._

1. Unzip the file and copy the contents to a location accessible to the Hyper-V server, such as a staging folder on the Hyper-V server.
2. From the Hyper-V Manager, connect to the Hyper-V host, right click the Hyper-V server name and click **Import Virtual Machine…**
3. The Import Virtual Machine wizard will open and you will be presented with the **Before You Begin** page. Click **Next >**
4. By clicking **Browse…**, locate the folder you copied the contents of the zip file to in Step 3 (`C:\Users\Perch\Downloads\PerchSensor-HyperV-v2.7.1-20220114\Virtual Machines`). Click Next > _You do NOT want to drill down into the folder, just select the folder as the vhdx and virtual machines will not be visible._
6. On the **Select Virtual Machine** page, select the Perch sensor (typically named something like _PerchSensor-HyperV-Latest_). Click **Next >**
7. On the **Choose Import Type** page, select **Copy Virtual Machine Image** **(create new unique ID)**. Click **Next >**
8. On the **Choose Destination** page you may choose an alternate storage location or choose to keep it default. Click **Next >**
9. On the **Choose Storage Folders** page you may choose an alternate storage location or choose to keep it default. Click **Next >**
10. On the **Summary** page, verify the values you have chosen and click **Finish**, this will begin the import of the virtual machine.

## Configuring A Hyper-V Virtual Sensor
1. Right click the newly imported virtual machine and choose **Settings…**
2. On the settings page, you will notice two network interfaces named **Network Adapter**
3. Connect the first network adapter to the <font color="orange"> management/production virtual switch</font>. This interface maps to <font color="orange"> eth0 </font> in the sensor.
4. Connect the second network adapter to the <font color="Purple"> mirror virtual switch </font> you have setup. This interface maps to <font color="purple"> eth1</font> in the sensor. Under Advanced settings ensure that Mirror mode: Destination is selected under the port mirroring section.
5. Click **OK** to save the settings and exit the Settings dialog

### Setting Up A Virtual Sensor

^789ada

Startup and connect to the imported virtual sensor. After which the sensor will be displayed with a black screen and the text perch-hyperv login: _

> [!Note]- The default user credentials
> 
> Username: <font color="Green"> perch</font>
> Password: <font color="Green"> prairiefire</font>

>[!Danger]- The default sudo user credentials
><font color="red"> THIS NEEDS TO BE CHANGED ASAP </font>
> 
> Username: <font color="green"> prairiefire </font>
> Password: <font color="green"> perch </font>

^2e19bf

_Note: If you lock out the user account with invalid login attempts you will need to wait 30 minutes before you can try again._

After first successful authentication you will be requested to create a new password. Please go to [Random Passphrase Generator](https://randompassphrasegenerator.com/), click Replace spaces with “-“, Add a number, Uppercase, and add a special character. Copy this password, documents it in the clients designated ITG page, and set it as the Perch credentials.

### Network Configuration
The sensor configuration wizard starts with the management network interface as shown below. The management network interface is the interface used to connect to the Perch cloud via the Internet.

![[net-01.png]]

Use the arrow keys to select the interface. Here we have selected the interface called **enp1s0**.

![[net-02.png]]

Then select whether or not the interface uses **DHCP**, here we have selected **No** and filled in the corresponding information.

![[net-03.png]]

Hit **OK** to continue. The settings are saved as we move on to the next section.

![[net-04.png]]

### Proxy Configuration
Proxy configuration is optional. If the management network interface does not need a proxy to access the Internet, select **No** then **OK** to continue.

![[proxy-01.png]]

If a proxy is needed, select **Yes** and fill in the necessary information as shown below.

![[proxy-02.png]]

In either case, hit **OK** to continue. The settings are saved as you continue to the next section.

![[proxy-03.png]]

### Monitored Network Interfaces
Here you can select which interfaces you wish to monitor, including the management interface you chose earlier (though this is not necessary).

The interfaces that should be monitored are the ones that have mirrored/spanned traffic that reproduces all your internal network traffic at an ingress/egress point. This is typically done with port mirroring on a managed switch.

![[mon-01.png]]

Here the **enp0s31f6** interface is marked as being monitored.

![[mon-02.png]]

Also in this section is the Suricata **HOME_NET**1 value, which indicates your local network subnets. The prepopulated default is appropriate in almost all cases.

As usual, hit **OK** to continue. The settings are saved as you continue to the next section.

![[mon-03.png]]

### Sensor Information
The next section covers some miscellaneous information about the sensor and its installation. This includes sensor name, to distinguish among a many-sensor installation, and geographic location.

![[info-01.png]]

For geographic location, you can enter your **Zip code**, **Country code** / **Postal code** or **Geohash**.

![[info-02.png]]

Hit **OK** when done. Settings are saved before moving to the final step.

![[info-03.png]]

### Register Your Sensor
Registration with the Perch cloud is the final step in the configuration process. To complete this step, generate an invite code from the Perch web application.

1.  To get your sensor invite code, login or register at: [app.perchsecurity.com](https://app.perchsecurity.com).
    
2.  For users installing their first sensor, click **Connect a Sensor**.

![[connect-a-sensor.png]]

3. For all other sensor installations, go to **Settings** then Sensors and click on the **Purple Plus icon**.

![[add-a-sensor.png]]

4. On the Device Invites page, create a new invite code with the **Purple Plus icon**.

![[new-invite-code.png]]

5. Enter the code you received from the Perch app into your sensor and hit **OK**. Please wait while your sensor completes registration as it may take a few minutes.

![[18.gif]]

![[19.gif]]

![[20.gif]]

6. Once completed, the sensor will be fully operational, though it may take some time before its internal processes have been fully initialized.

![[21.gif]]

# Log Shipper Deployment
This solution allows you to re-use old equipment. You will need to pay for a cloud license and the log shipper will communicate back to the cloud.

You will need to download and install the [Log Shipper](https://cdn.perchsecurity.com/downloads/perch-log-shipper-latest.exe) application on a Windows based pc.

```HTTPS
https://cdn.perchsecurity.com/downloads/perch-log-shipper-latest.exe
```

### Perch Log Shipper for Windows

_If you haven’t purchased Perch SIEM please reach out to your sales representative or contact us at sales@perchsecurity.com._

_If you need to download the Perch Log Shipper, please log into the Perch Application and navigate to Settings > Sensors and click “download the installer” at the top of the page._

_Supported OS versions - Windows 7 or Server 2012 R2 or greater._

### What's included in the Perch Log Shipper?

1. Winlogbeat - Winlogbeat sends your Windows Event Logs for processing and storage.
2. Auditbeat - Auditbeat sends audit data from the endpoint for processing and storage.
3. Sysmon - Sysmon is a free utility provided by Microsoft Sysinternals groups that provides a higher fidelity of insight into how your Windows systems are operating.

### Installing Perch Log Shipper

Locate and execute the downloaded installer.
![[Pasted image 20221014133336.png]]

Choose Next> and agree to the License Agreement.

![[Pasted image 20221014133402.png]]

Choose to install the base Perch Log Shipper and optionally Enable External Syslog

Collection

![[Pasted image 20221014133415.png]]

**Note about Syslog ports:** You only need to enable external Syslog collection on one device in the organization. This will be the destination you can send Syslog from firewalls, switches, routers, etc to. You will use the following ports

UDP Syslog: 42514

TCP Syslog: 42515

Perch doesn’t adjust the settings of your host-based firewall such as Windows Firewall. You will need to make a policy exception to allow the traffic inbound on those ports if your security policy blocks inbound traffic by default.

**Note about IIS Log collection:** If you enable the Syslog collection feature, it will also enable collecting IIS logs on the local server by default.

If you choose to send the logs to the Perch Sensor, select Send to Sensor and provide the IP address of the Perch Sensor.

If you choose to send the logs directly to the Perch Cloud, choose Send to Cloud (API) and provide the Client Token (API). You can obtain the Client Token by navigating in the Perch App to Settings > Sensors and copy the Agent Token from the top of the sensors settings page.

![[Pasted image 20221014133430.png]]

Click Finish to complete the setup.

Command Line Options

The Perch Log Shipper for Windows includes simple command-line options to deploy the Log Shipper silently and set the IP address or Client Token.

Examples:

`perch-log-shipper-latest.exe /qn OUTPUT="IP" VALUE="10.10.10.205"

This will install the Perch Log Shipper silently and set a Sensor IP address of 10.0.0.205.

`perch-log-shipper-latest.exe /qn OUTPUT="TOKEN" VALUE="abc-123-def-456"

This will install the Perch Log Shipper silently and set a Client Token to send the log data directly to the Perch Cloud.

### Installer notes
If there is a host-based firewall, network firewall, or network ACL between the endpoint and the Perch sensor, TCP/5044 will need to be allowed to traverse from the endpoint to the Perch sensor for data sent to the sensor. If the Cloud API option is chosen, TCP/443 will need to be allowed outbound to ingest.perchsecurity.com.

The installer writes data to C:\Program Files\Perch (or C:\Program Files (x86), for x86 based systems), C:\ProgramData\Perch and creates three services - perch-winlogbeat, perch-auditbeat, and sysmon. A fourth service named perch-filebeat will be created if you choose to enable external Syslog collection

# Sources and References
_These are the articles I used to create this document. This document has everything you need to set up a Perch Device with information that was acquired through e-mail. The online articles may not have some of the information that is included with this document._

Hyper-V Port Mirroring Article
- [https://perch.help/switches/setup-hyperv-portmirror/](https://perch.help/switches/setup-hyperv-portmirror/)

Import a Hyper-V virtual sensor
- [https://perch.help/sensors/setting-up-a-hyperv-sensor/](https://perch.help/sensors/setting-up-a-hyperv-sensor/)

Setting up a virtual sensor
- [https://perch.help/sensors/setting-up-a-virtual-sensor/](https://perch.help/sensors/setting-up-a-virtual-sensor/)

Adding a sensor
- [https://perch.help/sensors/adding-a-sensor/](https://perch.help/sensors/adding-a-sensor/)

Removing a sensor
- [https://perch.help/sensors/removing-a-sensor/](https://perch.help/sensors/removing-a-sensor/)

Perch Service Guide
- https://perch.help/onboarding/perch-service-guide/
