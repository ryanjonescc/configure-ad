<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />






<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)



<h2>Deployment and Configuration Steps</h2>

<p>In this lab, two virtual machines (VMs) will be set up within the same virtual network (VNET). One VM will function as a Domain Controller (DC), while the other will act as a Client machine. The DC’s IP address will be set to static since it provides Active Directory services to the Client. The Client machine will then be joined to the domain, and its DNS settings will be configured to use the DC as its DNS server.

  
  ![Screenshot_53](https://github.com/user-attachments/assets/dd4f51b7-c293-4a83-9757-5e63aa4a760a)

</p>
<p>
DC-1 must be assigned a static private IP address. Client-1 will connect to DC-1, and to verify connectivity, we will attempt to ping DC-1 from Client-1. Initially, the ping request will fail. To resolve this, ICMPv4 needs to be enabled in the firewall settings on DC-1. Once enabled, Client-1 will successfully ping DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
