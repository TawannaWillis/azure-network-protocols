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

- Step 1. Create Resource Group For VM1 and VM2
- Step 2. Observe ICMP Traffic
- Step 3. Observe SSH Traffic
- Step 4. Observe DHCP Traffic
- Step 5. Observe DNS Traffic
- Step 6. Observe RDP Traffic

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

First, create a resource group to house both virtual machines. Then, create the first VM, naming it VM1, and select Windows 10 Pro, version 22H2 as the operating system. Ensure the VM has at least 2 vCPUs and 16 GB of memory, set a custom username and password, and retain the default inbound port rules.

After configuring the initial settings, proceed through the setup pages until reaching the networking section. Azure will automatically generate a virtual network and subnet. Review the configuration and create the VM.




</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Create the second VM/VM2 using Ubuntu Server 20.04 LTS, following a similar process to the first VM/VM1, except we will switch the authentication type from SSH public key to password. *You can use the same username and password as VM1*. Proceed through the setup pages until reaching the networking section, where Azure will automatically use the virtual network and subnet from VM1. Review the configuration and create the VM.


</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
