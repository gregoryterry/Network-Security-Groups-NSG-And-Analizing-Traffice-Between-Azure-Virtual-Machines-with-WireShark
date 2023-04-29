# Network-Security-Groups-NSG-And-Analizing-Traffice-Between-Azure-Virtual-Machines-with-WireShark
In this lab I will create two Azure VMs and use Wireshark to analize traffic between the to VMs.

<p align="center">
<img src="" alt="WireShark logo"/>
</p>

<h1></h1>

<h2></h2>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- WireShark Packet Analyzer

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Linux Ubuntu Server

<h2>Summary</h2>

- Create two Azure virtual machines (Windows) (Linux)
- Log into the Windows VM “gtws01” with Remote Desktop
- Install WireShark on the Windows virtual machine
- Run wireshark and filter traffic by protocol
- Block ICMP in the Windows firewall, try to ping the Linux computer
- Enable ICMP in the Windows firewall, ping the Linux computer


<h4>Create Two Azure Virtual Machines</h4>

<p>In the web browser goto www.portal.azure.com
In the search bar type “virtual machines”
Create two virtual machines [+]  > Azure virtual machine

<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Create a new resource group named:  WireSharkLab
<p>

<p>Create a Window 10 VM
Use the following options:
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Make sure RDP port (3389) is selected and agree to the license term
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Leave the default settings for disk > go to networking tab > review + create
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Validation passed > create 
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>While deployment of the Windows VM is running, create the Linux VM

Type Virtual machine in the search box > create [+]  Azure VM
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Select the WireSharkLab resource group, put in the same zone as gtws01
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Select image:  Ubuntu server
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Administrator account
Select password for authentication > create a username and password
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Inbound rules
Select (ssh port 22)
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Select next > Leave the default disk settings > next for networking
**both virtual machines are on the save subnet
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Review + create > create
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>When deployment is complete, type “virtual machines”  in the search bar.  Here are the two new VMs
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<h4>Log into the Windows VM “gtws01” with Remote Desktop</h4>

<p>Click on gtws01 vm  > copy the public IP address
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Open Remote Desktop > paste the public IP address for gtws01 in the address field and enter your user name for this vm.
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Enter your password for the Windows VM
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Answer “yes” to have your pc discovered on the network
<p>

<h4>Install WireShark on the Windows virtual machine</h4>

<p>On the Windows VM > open Microsoft Edge > type “WireShark”  in the search bar > download the 64 bit version
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Browse to the wireshark exe file and install
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Follow the prompts and select your desired options
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Go to the desktop > start menu > right-click WireShark > more options > pin to taskbar > open wireshark from the taskbar
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<h4>Run wireshark and filter traffic by protocol</h4>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Select ethernet adapter to capture traffic
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<h5>Wireshark is now installed and running</h5>

<p>Wireshark displays:

No	 time		source		destination		protocol	length		info
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<h5>Here is a brief summary of the columns</h5>

<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>No. -Frame number from the beginning of the pcap. The first frame is always 1.
Time - Seconds broken down to the nanosecond from the first frame of the pcap. The first frame is always 0.000000.
Source - Source address, commonly an IPv4, IPv6, or Ethernet address.
Destination - Destination address, commonly an IPv4, IPv6, or Ethernet address.
Protocol - Protocol used in the Ethernet frame, IP packet, or TCP segment (ARP, DNS, TCP, HTTP, etc.).
Length - Length of the frame in bytes.
<p>

<p>The most common columns that are monitored are:

- Date & time in UTC
- Source IP and source port
- Destination IP and destination port
- HTTP host
- HTTPS server
- Info
<p>

<p>To hide or unhide a column, right-click the column and un-check the column in the list
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<h4> Run wireshark and filter traffic by protocol</h4>


<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<h4></h4>


<br />
