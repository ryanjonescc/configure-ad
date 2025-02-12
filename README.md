<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Preparing Active Directory Infrastructure in Azure</h1>
<p>In this lab, two virtual machines (VMs) will be set up within the same virtual network (VNET). One VM will function as a Domain Controller (DC), while the other will act as a Client machine. The DC’s IP address will be set to static since it provides Active Directory services to the Client. The Client machine will then be joined to the domain, and its DNS settings will be configured to use the DC as its DNS server.





<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)



<h2>Project Walk-through:</h2>

          First, navigate to Microsoft Azure and create a resource group.


![Screenshot_56](https://github.com/user-attachments/assets/ac47cb4e-b581-4ad5-a6e5-4323d5187ec6)

          Then create a virtual network



![Screenshot_57](https://github.com/user-attachments/assets/16e9bb40-4f79-476b-a21f-ddfe38cec927)








Once my resource group and network is created, I'll create and set up the virtual machine that will act as our Domain Controller. For the image, make sure you use Windows Server:

![Screenshot_58](https://github.com/user-attachments/assets/f40e834e-980b-420f-88c1-2279544c8e40)

</p>Now, I'll create another VM that will serve as the client. The image for this machine should be Windows 10, NOT Windows Server like I did for the previous machine:
<p>

  
  ![Screenshot_59](https://github.com/user-attachments/assets/fbf34ed7-829f-4dc4-8e28-1266980845ed)



  
DC-1 must be assigned a static private IP address. Client-1 will connect to DC-1, and to verify connectivity, we will attempt to ping DC-1 from Client-1. Initially, the ping request will fail. To resolve this, ICMPv4 needs to be enabled in the firewall settings on DC-1. Once enabled, Client-1 will successfully ping DC-1.
</p>

![Screenshot_60](https://github.com/user-attachments/assets/624f79cb-cea3-4942-a4bb-29292d455d4c)

<br />

<p>

  ![Screenshot_61](https://github.com/user-attachments/assets/52075de8-1a0c-4898-9fb4-be3599db7789)

</p>Next, I'll use Remote Desktop Connection to connect to the DC using its public IP and the log in credentials I created when setting up this machine: 
<p>Once I'm logged in, the following screen will appear with the Server Manager open. (If this isn't what you're seeing and instead it a regular windows desktop, you may have connected to the client VM instead or chose the wrong image when creating the DC)

</p>
<br />

<p>

 
  ![Screenshot_62](https://github.com/user-attachments/assets/942a1ab1-191b-42eb-b0f3-476d9f29d875)

</p>Next, I'm going to disable the firewall (you probably wouldn't do this in real lfe, but for the sake of this lab where nothing is at stake, I'll go ahead and do it). So, to disable the firewall I'll right click on the "Start" button and select "Run". Then type "wf.msc":




 
 ![Screenshot_63](https://github.com/user-attachments/assets/094576e0-48f8-43ee-9882-83c99ea69208)

Click on "Windows Defender Firewall Properties" then on the, "Domain Profile", "Private Profile, and the "Public Profile" tabs, turn the firewall state off:

![Screenshot_64](https://github.com/user-attachments/assets/74e8746c-73e8-493b-94a6-fffa45cc8bc5)

</p>Next, I need configure our clients DNS settings to the DC. To start, back in Azure, I'll grab the DCs private IP address:
<br />Then, I'll go to the network setting of the client machine. click on the NIC (Network Interface Card), go to settings, then DNS servers and switch from "Inherit from virtual network" to "Custom". Input the DCs private IP here and save:


![Screenshot_65](https://github.com/user-attachments/assets/1a7abbc2-237e-4370-87a2-bc7ea51b100f)
After that's saved, I'll restart the client machine:

Once the machine as restarted, I'll use Remote Desktop connection to connect to the client machine using its public IP and the log in credentials I created while setting up this machine:


Now that I'm logged in, I will open Powershell and attempt to ping the DC using the ping command and its private IP address. In my case it'll look like this. (If there is an error and the connection timed out, double check in Azure to make sure both of the machines are on the same virtual network. If they aren't this is likely causing the error and you'll need to set up the machine again on the same network):

![Screenshot_6](https://github.com/user-attachments/assets/0336b0d0-73dd-44ef-8465-e9cbe3e527e9)

While I'm here I can double check that the DNS server settings are pointing to the DC. I'll run "ipconfig /all" and look for the "DNS Servers" and it should point to our DC if everything is set up properly:

![Screenshot_67](https://github.com/user-attachments/assets/5087451f-3dee-4873-a5e6-1e1201bf87b5)

Active Directory Infrastructure is Now Prepared!

<b>We've successfully created two VMs (Virtual Machines), one running Windows Server, to act as a Domain Controller. The other VM as a client, running Windows 10. Don't forget: In later projects I will deploy AD, run a script that will create users in the domain, which I can log into from the client VM, then manage the accounts and update the group policies, all to simulate a real life environment!  </b>
