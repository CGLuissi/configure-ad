            p align="center">
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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1.) We're going to start off our lab by creating 2 different virtual machines- one of which will be our domain controller (DC-1) and the other will be the client machine (Client-1). Start off by heading to the azure portal and selecting "create a resource" and select virtual machine. Click "create new" under the resource group dropdown box, and name this group "AD-Lab". Name your virtual machine "DC-1", and select Windows Server 2022 as the image type. In the Size tab, make sure to select a size that has at least 2 vcpus. Any Region should be fine as long as both DC-1 and Client-1 share the same. Make sure to keep note of the username and password as well. Scroll down and check off the box that says "use an existing windows server license?" and then confirm. Now click Review + Create and your first virtual machine will be created after a short period.


2.) 



<img width="567" alt="Vnet step" src="https://github.com/CGLuissi/configure-ad/assets/143234913/b58a76a3-5c6f-4888-9230-47c7b2bb0a53">



3.) Wait about 10 minutes for DC-1 and its virtual network to be created and then create another resource. This time name the virtual machine "Client-1" and put it in the AD-Lab resource group. Use Windows 10 Pro as the image type and use 2 vcpus as the size. Keep note of your Username and Password here as well, and then click to confirm you have an existing Windows 10 license. After clicking Review + Create and just before clicking Create, go to the Networking Tab and make sure your new VM is in the same vnet/subnet as DC-1. You should have a vnet that says DC-1/vnet or something similar.




4.) On the virtual machines status page, click DC-1 and go to the Networking tab on the lefthand side under Settings. From here, click on the Network Interface and then on IP Configurations. Now click on ipconfig1 and change the IP setting to Static instead of Dynamic. 


  
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
