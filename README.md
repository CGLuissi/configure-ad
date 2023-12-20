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


<img width="818" alt="Step 4 1" src="https://github.com/CGLuissi/configure-ad/assets/143234913/95e840a4-b447-48af-9a1e-774347933242">




4.) On the virtual machines status page, click DC-1 and go to the Networking tab on the lefthand side under Settings. From here, click on the Network Interface and then on IP Configurations. Now click on ipconfig1 and change the IP setting to Static instead of Dynamic. 


<img width="761" alt="Step5" src="https://github.com/CGLuissi/configure-ad/assets/143234913/c5b2df58-e3c8-433d-9e9d-73bcd564a248">


<img width="340" alt="Step5 1" src="https://github.com/CGLuissi/configure-ad/assets/143234913/11e1eace-ad0e-446f-a365-666f87eab087">




5.) Find the public IP address for Client-1 on the information tab. On the remote desktop program, enter the public IP and select "more choices" on the next prompt; select "choose a different account" and log in with the username and password for Client-1. Once logged in, select "yes" on the prompt that asks if you want to allow your pc to become discoverable on the network.


<img width="832" alt="Step6" src="https://github.com/CGLuissi/configure-ad/assets/143234913/166805e2-52ae-4115-bf66-72bfdd5638a6">



6.) Head back to the information page for DC-1 and note the private IP address; we are going to test the connection between our 2 VMs by sending a message to our domain controller. Back in Client-1, open up the command prompt application and type this command: ping -t (DC-1's Private IP). The command ping is used to verify that we can reach our target computer, and the -t suffix allows for an automatic, perpetual ping that is stopped when we manually end it. If successful, we should recieve a response message indicating that there is a working connection between our two systems. 


<img width="274" alt="Step6 1" src="https://github.com/CGLuissi/configure-ad/assets/143234913/9c8e0e5e-a028-4a76-bbc2-0b4037ac90a2">



7.) We can see that there is a response "Request timed out" meaning that we aren't able to reach DC-1. Now, we must get the Public IP address for DC-1 and open another instance of remote desktop to see if we can resolve this issue. 


  
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
