# Analyzing Traffic Between Azure Virtual Machines with WireShark
<h5>In this lab I will create two Azure VMs and use Wireshark to analize traffic between the two VMs.</h5>

<p align="center">
<img src="https://i.imgur.com/qYqLe8K.jpg" alt="WireShark logo"/>
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
- Block ICMP in the Linux VM, try to ping the Linux VM from the Windows VM
- Enable ICMP in the Windows firewall, ping the Linux computer


<h4>Create Two Azure Virtual Machines</h4>

<p>In the web browser goto www.portal.azure.com
In the search bar type “virtual machines”
Create two virtual machines [+]  > Azure virtual machine

<P>
<img src="https://i.imgur.com/FnIeV0E.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<P>
<p>Create a new resource group named:  WireSharkLab
<p>

<p>Create a Window 10 VM
Use the following options:
<p>
<img src="https://i.imgur.com/EUdlV2Y.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<P>
<img src="https://i.imgur.com/DRwoo9i.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<P>
<img src="https://i.imgur.com/irH6tSP.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</P>
<img src="https://i.imgur.com/DRwoo9i.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<P>
<img src="https://i.imgur.com/irH6tSP.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

</P>
<p>Make sure RDP port (3389) is selected and agree to the license term
<p>
<img src="https://i.imgur.com/eawrNX0.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<P>
<p>Leave the default settings for disk > go to networking tab > review + create
<p>
<img src="https://i.imgur.com/ikbaHaA.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Validation passed > create 
<p>
<img src="https://i.imgur.com/nCoxn15.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>While deployment of the Windows VM is running, create the Linux VM
<p>
	
Type Virtual machine in the search box > create [+]  Azure VM
<p>
<img src="https://i.imgur.com/5LVOUmX.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<P>
	
<p>Select the WireSharkLab resource group, put in the same zone as gtws01
<p>
<img src="https://i.imgur.com/dO9MDeR.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Select image:  Ubuntu server
<p>
<img src="https://i.imgur.com/5Nd0tC0.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<h4>Administrator account</h4>h4>
<p>
Select password for authentication > create a username and password
<p>
<img src="https://i.imgur.com/l5hNpT3.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Inbound rules
Select (ssh port 22)
<p>
<img src="https://i.imgur.com/ehVDVWB.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
	
<p>Select next > Leave the default disk settings > next for networking
**both virtual machines are on the save subnet
<p>
<img src="https://i.imgur.com/Aywv8Zb.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
	
<p>Review + create > create
<p>
<img src="https://i.imgur.com/1ZgspGp.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>When deployment is complete, type “virtual machines”  in the search bar.  Here are the two new VMs
<p>
<img src="https://i.imgur.com/2L5jPoB.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>
	
<h4>Log into the Windows VM “gtws01” with Remote Desktop</h4>

<p>Click on gtws01 vm  > copy the public IP address
<p>
<img src="https://i.imgur.com/Fm627Rj.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Open Remote Desktop > paste the public IP address for gtws01 in the address field and enter your user name for this vm.
<p>
<img src="https://i.imgur.com/SgdOBxc.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

<p>Enter your password for the Windows VM
<p>
<img src="https://i.imgur.com/24MnZTD.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>
<p>
<img src="https://i.imgur.com/s9tQ3ZM.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>

<p>Answer “yes” to have your pc discovered on the network
<p>

<h4>Install WireShark on the Windows virtual machine</h4>

<p>On the Windows VM > open Microsoft Edge > type “WireShark”  in the search bar > download the 64 bit version
<p>
<img src="https://i.imgur.com/BDx0PLQ.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/PhUwoOS.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Browse to the wireshark exe file and install
<p>
<img src="https://i.imgur.com/nb6YlcQ.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<p>
<img src="https://i.imgur.com/yAvgz30.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

<p>Follow the prompts and select your desired options
<p>
<img src="https://i.imgur.com/yAvgz30.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<p>
<img src="https://i.imgur.com/TnTmDRE.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<p>
<img src="https://i.imgur.com/LOJbzhB.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<p>
	
<p>Go to the desktop > start menu > right-click WireShark > more options > pin to taskbar > open wireshark from the taskbar
<p>
<img src="https://i.imgur.com/ZXgBL87.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/pAqfvgE.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Select ethernet adapter to capture traffic
<p>
<img src="https://i.imgur.com/QtAoRYh.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<h5>Wireshark is now installed and running</h5>

<p>Wireshark displays:
<P>
	
<P>No	<P></P> time		<P></P>source		<P></P>destination		<P></P>protocol	<P></P>length		<P></P>info
<P>
<p>
<img src="https://i.imgur.com/edUGvin.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<h5>Here is a brief summary of the columns</h5>

<img src="https://i.imgur.com/JRvdduO.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>No. -Frame number from the beginning of the pcap. The first frame is always 1.<P></P>
<P></P>Time - Seconds broken down to the nanosecond from the first frame of the pcap. The first frame is always 0.000000.
<P></P>Source - Source address, commonly an IPv4, IPv6, or Ethernet address.
<P></P>Destination - Destination address, commonly an IPv4, IPv6, or Ethernet address.
<P></P>Protocol - Protocol used in the Ethernet frame, IP packet, or TCP segment (ARP, DNS, TCP, HTTP, etc.).
<P></P>Length - Length of the frame in bytes.
<p>

<h4>The most common columns that are monitored are:</h4>

- Date & time in UTC
- Source IP and source port
- Destination IP and destination port
- HTTP host
- HTTPS server
- Info
<p>

<p>To hide or unhide a column, right-click the column and un-check the column in the list
<p>
<img src="https://i.imgur.com/vtVjYKi.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<h4> Run wireshark and filter traffic by protocol</h4>

<h5>Filter ICMP traffic</5>

<p>In the filter field type: ICMP	*** this is the protocol that ping uses
<p>
<img src="https://i.imgur.com/vS364yr.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<p>Get the private IP address for the Linux VM, gtws02. 
 <p>
<img src="https://i.imgur.com/RVSZvPK.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
   
<p>Using the Windows VM, open cmd prompt  and ping the Linux VM private IP address
 <p>
   <img src="https://i.imgur.com/TGLBRDb.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>
   
<p>Ping 10.0.0.5
<p>
  <img src="https://i.imgur.com/gOqoMNi.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<h5>Go to the wireshark console to see the traffic that was captured from the ping</h5>

<p>You can see the request from the source address which is the Windows VM with IP address 10.0.0.4
The reply came from the Linux VM with the IP address 10.0.0.5
The protocol is ICMP
This is an echo request (Ping)
<p>
<img src="https://i.imgur.com/6cIie1q.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<h5>Ping a website</h5>

<p>From the cmd prompt, ping google.com
<p>
<img src="https://i.imgur.com/rIPRZqq.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
  <p>Go to the wireshark console
We can see that the source request IP 10.0.0.4 is the Windows VM
The reply IP is different.  This is the google.com IP address
<p>
<img src="https://i.imgur.com/2u5CSc6.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>
	
<h4>Block ICMP in the Linux VM, try to ping the Linux VM from the Windows VM</h4>

<p>**we can do this in the Azure console

  Select the Linux VM > search for “ Network Security Groups”
<p>
<img src="https://i.imgur.com/QBN1Xud.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
<p><img src="https://i.imgur.com/I5jf8b1.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
</p>  

<p>Select inbound security rules > add > fill out the fields as follows: > add
  <p>
<img src="https://i.imgur.com/bNHvmCK.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>    
<img src="https://i.imgur.com/SzkwCIF.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
    
<p>Here is the new rule, it denies ping
<p>
<img src="https://i.imgur.com/Ga11iqU.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<p>Go back to the cmd prompt on the Windows vm and ping the private IP 10.0.0.5 again
The request timed out because the firewall for VM2 is blocking the ICMP request
<p>
<img src="https://i.imgur.com/FJJ8xuz.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<p>Go to Wireshark to view the traffic from this request
There is only a request from 10.0.0.4 and no reply from 10.0.0.5
<p>
<img src="https://i.imgur.com/2TfSBbq.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>On the Windows VM, ping 10.0.0.5
  
      Ping 10.0.0.5 -t		***the ping should timeout
  <p>
 <img src="https://i.imgur.com/AmXevoo.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Go to wireshark to check the ICMP traffic, 10.0.0.4 should display “request” with no reply from 10.0.0.5
<p>
  <img src="https://i.imgur.com/yjnSi1v.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

 <p>Go to the Azure Linux VM (GTWS02) > Networking > Inbound Port Rules > click “block ICMP” rule
   <p>
<img src="https://i.imgur.com/VMfRNQg.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
     
<p>Under Action select “Allow”		** this will enable ICMP traffic through the firewall
<p>
<img src="https://i.imgur.com/HipT9i2.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/f7TeUnm.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<p>ICMP is allowed
 <p>
<img src="https://i.imgur.com/qKIw23R.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
   
<p>Check the ping status and Wireshark traffic
<p>
  <img src="https://i.imgur.com/J677lj0.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<p>10.0.0.4 is receiving a reply from 10.0.0.5
<p>
  <img src="https://i.imgur.com/lDFHD6d.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>

 
<h5>Filter SSH traffic</h5>

<p>Set the Wireshark filter for SSH
<p>
  <img src="https://i.imgur.com/I3R6uV1.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<p>Open Powershell as an administrator

Log on to the Linux VM GTWS02 with the following command:

	Ssh gterry@10.0.0.5		** the username and Private IP address
	Answer yes to the logon question and enter the password for VM2
<p>
  <img src="https://i.imgur.com/oZIqy6Q.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<p>I am logged on to the Linux VM
<p>
  <img src="https://i.imgur.com/ljedtmf.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>
 
<p>On the Windows VM, go to Wireshark to see the SSH traffic 
  <p>
 <img src="https://i.imgur.com/1fqddtP.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
 
<p>Go back to Powershell, type “exit” to close SSH
<p>
 <img src="https://i.imgur.com/N5GpaDc.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<p>

 
<h5>Filter TCP Traffic</h5>

<p>Here is the traffic for my Remote Desktop connection (RDP) on port 3389
<p>
    <img src="https://i.imgur.com/GQHBUZw.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<h5>Filter DNS Traffic</h5>

<p>Type "Dns" in the filter bar
  <p>
<img src="https://i.imgur.com/h3V133B.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
    
<p>In powershell do an nslookup for google.com
Nslookup google.com
<p>    
     <img src="https://i.imgur.com/c4mFjl0.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<p>Check the DNS traffic in Wireshark
<p>
     <img src="https://i.imgur.com/epUjtfZ.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>I looked up the google.com IP address and the query was captured by Wireshark
<p>

<h5>Follow the same procedure to filter  “UDP” traffic</h5>

<img src="https://i.imgur.com/jU2tjyq.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Wireshark show I got a response from the DNS server on port 53 for UDP protocol
<p>     
     <img src="https://i.imgur.com/sJadqXs.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<h5>Filter RDP Traffic<h/5>

<p>Enter:  tcp.port == 3389  or type:  rdp

Wireshark is displaying traffic from RDP port 3389
<p>
     <img src="https://i.imgur.com/t5KbPMl.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<h5>Filter DHCP Traffic</h5>
  
<p>In Powershell > ipconfig /renew		** request a new IP address from the DHCP server
<p>
 <img src="https://i.imgur.com/trehXQk.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>	    
  
<p>Looking inside the Wireshark console, we can see that my VM 10.0.0.4 sent a DHCP Request and the DHCP server sent a reply called DHCP ACK.
<p>
     <img src="https://i.imgur.com/mY52d2F.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Lets try: ipconfig /release	*** the will free the current IP address
<p>
<img src="https://i.imgur.com/mY52d2F.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>You may need to restart your VM, if possible DHCP will give you the same address
<p>
<img src="https://i.imgur.com/5tFFj1k.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  
<p>Log back into the VM
<p>
<img src="https://i.imgur.com/ilicIRz.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<h4>Conclusion</h4>
 
<p>In this lab I demonstrated how Wireshark can capture network traffic by filtering protocols or by selecting a specific port.
I also showed how Wireshark can display blocked requests that have been denied by  the VM firewall.
<p>


