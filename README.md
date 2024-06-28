<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
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
The first step is to create a Virtual Machine on Azure.
Select the operating system or image as Windows 10 Pro, version 22H2</p>
<p>
<img width="800" src="https://imgur.com/I1pVEtM.png">

<p>
</p>
<p>
<strong> NOTE: Set the size to at least 2 vcpus and 16 GIB memory. Keep in mind of the virtual network VM-1 creates, this will be used for VM-2. 

<p>
</p>
<p>
<h3>&#9313; Create a second Virtual Machine on Azure </h3>
<p>The next step is to create another Virtual Machine on Azure. This time using Linux as the image, also shown below as Ubuntu Server 20.04 LTS - x64 Gen 2.</p>
<img width="700" src="https://imgur.com/Jaa9wz6.png">

</p>
<p>
<h3>&#9314; Connect to your VM-1 using the Remote Desktop app</h3>
<p>Open your Remote Desktop app and paste the VM-1's IP address, then login credentials used to create the VM.</p>
<p>
<img width="500" src="https://imgur.com/UNSM5uA.png">

<img width="500" src="https://imgur.com/FIK7DKP.png">

</p>
<p>
<h3>&#9315; Install Wireshark in Browser </h3>
<p>Within your Windows 10 VM, type www.wireshark.org in browser, then install Windows x64 Installer</p>
<p>
<img width="500" src="https://imgur.com/DRodXGX.png">

</p>
<br />
<h3>&#9316; Filter for ICMP Traffic </h3>
<p> Open Wireshark and filter for ICMP traffic. Click on the blue shark fin in the corner of the app, then proceed to type icmp within the green search bar.</p>
<p> <img width="750" src="https://imgur.com/lQugkgE.png">
<br>
<br> <img width="750" src="https://imgur.com/kjnfpQI.png">

<br />
<h3>&#9317; Ping Private Address of VM-2 from within Windows 10 </h3>
<p> Open Wireshark and filter for ICMP traffic. Click on the blue shark fin in the corner of the app, then proceed to type icmp within the green search bar.</p>
<br> 
<img width="550" src="https://imgur.com/qSnkdeu.png">

<br> 
<br> 
Open Command Line or Powershell and use the Private IP Address of VM-2. Type "ping 10.0.0.5" to observe ICMP traffic within Wireshark
<br> 
<br />
<img width="650" src="https://imgur.com/NzVRif2.png">
<br> 
<br> 

Now we will attempt to ping a website such as Google and observe ICMP traffic. Type "ping www.google.com -4" 

<br />
<img width="650" src="https://imgur.com/r3oVwgP.png">

<br />
<h3>&#9318; Initiate Perpetual Ping from VM-1 to VM-2 </h3>
<p> Type "ping 10.0.0.5 -t" this will send a non-stop ping between the two virtual machines.</p>
<br> 
<img width="550" src="https://imgur.com/4ebYoKg.png">
<br>
<br> <img width="650" src="https://imgur.com/mqwyvWl.png">

