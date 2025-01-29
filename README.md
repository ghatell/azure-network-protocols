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

- Virtual Machine Setup
- Observing ICMP Traffic
- Configuring a Firewall (Network Security Group)
- Observing SSH Traffic
- Observing DHCP Traffic
- Observing RDP Traffic
- Lab Cleanup

<h2>Actions and Observations</h2>

<p>
<img width="867" alt="1" src="https://github.com/user-attachments/assets/8a835693-510f-43fb-bb50-9dc8c2785cda" />
</p>
<p>
In this lab, we began by setting up virtual machines in Azure. We created a Resource Group to organize resources and deployed a Windows 10 Virtual Machine (VM) within this group, allowing Azure to automatically create a Virtual Network (VNet) and Subnet. Next, we added a Linux (Ubuntu) VM, ensuring it was part of the same Resource Group, VNet, and Subnet as the Windows VM. Authentication for the Linux VM was configured using a username and password. These VMs were kept active for subsequent parts of the lab.
</p>
<br />

<p>
<img width="1245" alt="2 1" src="https://github.com/user-attachments/assets/058f41af-4391-4a7a-983c-bd04a6d13b17" />
</p>
<p>
The second part focused on observing ICMP traffic. We connected to the Windows 10 VM via Remote Desktop and installed Wireshark to capture network packets. Filtering for ICMP traffic, we retrieved the private IP address of the Ubuntu VM and initiated a ping from the Windows VM to the Ubuntu VM, observing the requests and replies in Wireshark. We also tested pinging a public website, such as www.google.com, from the Windows VM and analyzed the ICMP traffic generated.
</p>
<br />

<p>
<img width="1083" alt="3" src="https://github.com/user-attachments/assets/84c904ef-eb4e-4fdf-a938-c290f2c79a47" />
<img width="1236" alt="3 1" src="https://github.com/user-attachments/assets/00ec0eeb-a687-4b21-b27f-25be7a1158f9" />
</p>
<p>
In the third part of the lab, we explored configuring firewalls using Network Security Groups (NSGs). First, we initiated a continuous ping from the Windows VM to the Ubuntu VM and then disabled inbound ICMP traffic in the NSG associated with the Ubuntu VM. This caused the ping requests to fail, as observed in both the command line and Wireshark. Re-enabling ICMP traffic restored the pings, and we verified the traffic resumption in Wireshark.
</p>
<br />

<p>
<img width="1180" alt="4" src="https://github.com/user-attachments/assets/41def1df-a43a-4e4a-8e9e-2b8b130ba77f" />
</p>
<p>
Next, we analyzed SSH traffic by filtering for it in Wireshark and using PowerShell on the Windows VM to SSH into the Ubuntu VM via its private IP address. Commands entered during the SSH session generated observable traffic in Wireshark, and we exited the session to stop the flow.
</p>
<br />

<p>
<img width="1194" alt="5" src="https://github.com/user-attachments/assets/9ec79eb2-3184-47b4-a315-a53ec8f36120" />
</p>
<p>
We also observed DHCP traffic by filtering for it in Wireshark and running the ipconfig /renew command in PowerShell to request a new IP address. This action generated DHCP traffic, which was captured and analyzed in Wireshark.
</p>
<br />

<p>
<img width="1188" alt="6" src="https://github.com/user-attachments/assets/8a2e1cfd-d8dc-4db7-81bf-5a335c56820e" />
</p>
<p>
Finally, we analyzed DNS traffic by using nslookup in the Windows VM command line to resolve the IP addresses of google.com and disney.com. The DNS queries and responses were visible in Wireshark. 
</p>
<br />

<p>
<img width="1089" alt="7" src="https://github.com/user-attachments/assets/83c00ea3-c4a5-4c4d-9679-3a7d2fbe80ea" />
</p>
<p>
Additionally, we filtered for RDP traffic using tcp.port == 3389 and observed the continuous stream of traffic caused by the live Remote Desktop Protocol connection between the Windows VM and the local machine.
</p>
<br />

<p>
<img width="773" alt="8" src="https://github.com/user-attachments/assets/e3113b12-d7b1-4bca-ba12-3fcf3dd6b9c4" />
</p>
<p>
To conclude the lab, we performed cleanup by closing the Remote Desktop connection to the Windows VM and deleting the Resource Group created at the start, ensuring all associated resources were removed to prevent additional charges. This lab demonstrated the setup of Azure VMs, the use of Wireshark to analyze network traffic, and the management of firewall settings using NSGs.
</p>
<br />
