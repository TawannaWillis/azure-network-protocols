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
After connecting to the Windows VM or VM1 via Remote Desktop Connection using its public IP, install Wireshark to inspect network traffic. In Wireshark, filter for ICMP traffic and use PowerShell to ping the Ubuntu VM (VM2) using its private IP address and google.com. Then, execute a perpetual ping to VM2 using the command "ping -t [IP address]" to observe network security group behavior. I also applied a security rule to the Ubuntu VM's network settings in Azure to block ICMP traffic, making sure the new rule took precedence over SSH with a priority over (300) Back on the Windows VM, I saw the ping attempts failing, confirming the block was working. Then, I allowed ICMP traffic again by removing the security rule, and perpetual ping resolved without timing out. 


</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Next, I decided to examine SSH traffic. I logged into the Ubuntu server using PowerShell's ssh command and filtered Wireshark traffic with `tcp.port == 22`. Every command I executed on the Ubuntu server was captured in Wireshark, allowing me to monitor the session in real-time.

</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

I logged out of the Ubuntu server to focus on DHCP traffic. To generate some activity, I ran the `ipconfig /renew` command on my VM, which briefly disconnected me while requesting a new IP address. After reconnecting, I could see the DHCP traffic captured in Wireshark, giving me a clear view of the process.

</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>





To examine DNS traffic, I applied the filter `udp.port == 53` in Wireshark. Using the command prompt, I executed `nslookup` queries for google.com and disney.com. This allowed me to observe the DNS lookup process for these popular domains, with Wireshark displaying the corresponding queries and responses in real-time.


</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Rounding out my lab, I observed RDP traffic using the Wireshark filter `tcp.port == 3389`. This filter captured continuous traffic since RDP constantly transmits data to provide a live stream from my personal computer to the Azure-hosted VM.


<h2>Key Takeaways</h2>


I gained a practical and hands on understanding of cloud networking with this lab, by setting up Windows and Ubuntu VMs in Azure. Using Wireshark, I got to see various network protocols in action - from basic pings to SSH connections. I played around with security rules, watching how they affected traffic between my VMs. I gained a much needed visual understanding on how DHCP, DNS, and RDP work behind the scenes. By the end, I felt like I'd gotten a real taste of what it's like to manage and secure a cloud network. 


