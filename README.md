<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
This tutorial is focused on examining network traffic between Azure Virtual Machines using Wireshark. It involves creating and configuring VMs, observing various network protocols (ICMP, SSH, DHCP, DNS, RDP), and experimenting with Network Security Groups to manage and secure traffic. This project provides hands-on experience in network traffic analysis and the practical application of network security concepts within Azure environments. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP,SSH,DHCP,DNS,RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Resource Group
- Virtual Network
- Subnet (Windows & Linux)
- Network Security Group

<h2>Actions and Observations</h2>

<h3>&#9312; Create a Virtual Machine on Azure</h3>
The first step is to create a Virtual Machine on Azure; 
select the operating system or image as Windows 10 Pro, version 22H2</p>
<p>
<img width="800" src="https://imgur.com/I1pVEtM.png">

<p>
</p>
<p>
<strong> NOTE: Set the size to at least 2 vcpus and 16 GIB memory. Keep in mind of the virtual network VM-1 creates, this will be used for VM-2

<p>
</p>
<p>
<h3>&#9313; Create a second Virtual Machine on Azure </h3>
<p>The next step is to create another Virtual Machine on Azure. This time using Linux as the image, also shown below as Ubuntu Server 20.04 LTS - x64 Gen 2</p>
<img width="800" src="https://imgur.com/Jaa9wz6.png">

</p>
<p>
<h3>&#9314; Connect to your VM-1 using the Remote Desktop app</h3>
<p>Open your Remote Desktop app and paste VM-1's IP address, then login using the credentials made to create the virtual machine</p>
<p>
<img width="500" src="https://imgur.com/UNSM5uA.png">
<br />
<br />
<img width="500" src="https://imgur.com/FIK7DKP.png">

</p>
<p>
<h3>&#9315; Install Wireshark</h3>
<p>Within your Windows 10 VM, type www.wireshark.org in browser, then download and install Windows x64 Installer</p>
<p>
<img width="400" src="https://imgur.com/DRodXGX.png">

</p>
<br />
<h3>&#9316; Filter for ICMP Traffic </h3>
<p> Open Wireshark and filter for ICMP traffic. Click on the blue shark fin in the corner of the app, then proceed to type "icmp" within the green search bar</p>
<p> <img width="650" src="https://imgur.com/lQugkgE.png">
<br>
<br> <img width="650" src="https://imgur.com/kjnfpQI.png">

<br />
<h3>&#9317; Ping Private Address of VM-2 from within Windows 10 </h3>
<p> Retrieve the private IP address of VM-2 based back in the Azure portal</p>
<br> 
<img width="450" src="https://imgur.com/qSnkdeu.png">

<br> 
<br> 
Once you've located the IP address, open Command Line or Powershell and use the Private IP Address of VM-2. Type "ping 10.0.0.5" to observe ICMP traffic within Wireshark
<br> 
<br />
<img width="850" src="https://imgur.com/NzVRif2.png">
<br> 
<br> 

Now we will attempt to ping a website such as Google and observe ICMP traffic. Type "ping www.google.com -4" 

<br />
<img width="850" src="https://imgur.com/r3oVwgP.png">

<br />
<h3>&#9318; Initiate Perpetual Ping from VM-1 to VM-2 </h3>
<p> Type "ping 10.0.0.5 -t" this will send a non-stop ping between the two virtual machines</p>
<br> 
<img width="850" src="https://imgur.com/4ebYoKg.png">
<br>
<br> <img width="850" src="https://imgur.com/mqwyvWl.png">

<br />
<h3>&#9319; Disable ICMP traffic on VM-2's firewall </h3>
<p> Once we block ICMP traffic, we should see that the perpetual ping stops working. Once that traffic is observed, the next step is to re-enable ICMP</p>

- This exercise allows for a better understanding of how firewalls work and a general basic knowledge of networking
  
<br />

In Azure portal, search Network security groups -> VM-2 -> Settings (Inbound security rules) 
- Add a rule with Protocol (ICMP), Action (Deny), Priority (200), and Name (DENY_ICMP_PING_FROM_ANYWHERE)

<br />
<img width="450" src="https://imgur.com/SRGfi7o.png">
<br />
<img width="450" src="https://imgur.com/gS5dtHg.png">
<br />
<img width="450" src="https://imgur.com/57TaBog.png">

<h3>&#9320; Observe disabled traffic in Wireshark & Powershell</h3>
<br> 
<img width="800" src="https://imgur.com/FQiWzOk.png">
<br> 
<img width="800" src="https://imgur.com/pWjDGU7.png">

<br> 
<h3>&#9321; Re-Enable ICMP traffic</h3>
In Azure portal, go back and do the previous step. This time, we will re-enable ICMP traffic and observe the perpetual ping to continue

- Network security groups -> VM-2 - Settings (Inbound security rules)
- Click on the DENY_ICMP_PING rule and edit the Action to "Allow" as shown below

<br />
<img width="650" src="https://imgur.com/LwZOdlQ.png">
<br />
<img width="650" src="https://imgur.com/wJlRRQS.png">

<br />
<br />
Back in Powershell, we can see that the command-line has began it's nonstop ping between both virtual machines. This means the network security has come into affect and allowed VM-1 to receive responses from VM-2 again. Press [control + c] to stop the ping  

<br />
<br />
<img width="650" src="https://imgur.com/7ofPdfd.png">

<br> 
<h3>&#9322; Explore SSH traffic</h3>
The next step is to now filter by SSH (secure shell). This essentially serves it's purpose for remote access, similar to Remote Desktop
<br />
<img width="1050" src="https://imgur.com/DC98MNI.png">

<br />
<br />

Instead of pinging VM-2, we will SSH into the second virtual machine through VM-1. For this case, the login credential is "labuser". Type "ssh labuser@10.0.0.5" 

<br />
<br />
<img width="850" src="https://imgur.com/Xf6VFiH.png">

<br />
<br />

This allows us to remotely access VM-2. In the command line, we will write a few Linux codes and observe the traffic being produced in Wireshark
- Linux codes
  - id
  - uname -a
  - pwd
  - ls -lasth
  - touch hi.txt
  - ls -lasth
 
To sum up the reasoning for these commands, the function is to list the folders and files in the current directory 

<br />
<img width="850" src="https://imgur.com/dHgz5w3.png">

<br />
<br />

<img width="850" src="https://imgur.com/btVeirD.png">

<br />
<br />
<img width="850" src="https://imgur.com/1HXz9xJ.png">

<br />
<br />

Another way to filter through SSH traffic is through "tcp.port == 22" in the green search bar of Wireshark. This is possible because SSH uses Port 22. We can see in the picture below that tcp port 22 shows SSH traffic. Secure Shell (ssh) essentially serves as the more direct approach

<br />
<img width="850" src="https://imgur.com/8bDJmgj.png">

<br> 
<h3>&#9323; Observe DHCP traffic through Wireshark</h3>
DHCP is essential because it assigns IP addresses and network settings to devices, enabling efficient communication

<br> 
- In Wireshark, type "dhcp" in the search bar in order to filter for this specific traffic
<br> 
<br />
<img width="1050" src="https://imgur.com/ns3bZGW.png">
<br> 
<br />
- Next, in Powershell we will request a new IP address from the DHCP server. To do this type "ipconfig /renew" refreshing the network configuration for the device. You should see some traffic appear in Wireshark
<br> 
<br />
<img width="850" src="https://imgur.com/usuc3SM.png">

<br> 
<h3>&#9324; Filter through DNS traffic</h3>
DNS translates human-friendly names into IP addresses that computers use to identify each other on the network 
<br> 
<br />
- Once more search "dns" in Wireshark; you'll see some DNS traffic already running. Refresh by selecting the green shark fin to clear traffic spamming the server

<br> 
<br />
<img width="1050" src="https://imgur.com/AX41Nuy.png">
<br> 
<br />
- In the command line, type in "nslookup www.google.com". This queries the DNS to obtain the IP address associated with Google
<br> 
<br />
<img width="850" src="https://imgur.com/PV7SPIV.png">

<h2> Final Thoughts </h2>

A project like this allows for one to understand the intricacies of network traffic analysis, the importance of various network protocols, and how to use tools like Wireshark for diagnostics. It also demonstrates the significance of network security through hands-on experience with Network Security Groups (NSGs), highlighting how to manage and secure network traffic effectively. This knowledge is crucial for maintaining secure and robust network environments. 






