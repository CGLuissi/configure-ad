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



<img width="558" alt="Step 7 2" src="https://github.com/CGLuissi/configure-ad/assets/143234913/351cb8cf-6d69-4ca1-96f9-6ae2a0e3c268">


7.) We can see that there is a response "Request timed out" meaning that we aren't able to reach DC-1. Now, we must get the Public IP address for DC-1 and open another instance of remote desktop to see if we can resolve this issue. Within DC-1's task bar search , type "wf.msc" to open Windows Firewall. Select "inbound rules" and enlarge the VM window. Look for these 2 rules: "Core Networking Diagnostics ICMP Echo Request" (IPv4) and right click them, then click enable rule. The Internet Control Message Protocol(ICMP) is used to diagnose network communication issues and analyze health; however, Windows Firewall settings block pings by default. By enabling the 2 settings, we can receive a response to our ping on Client-1 and you can cancel the perpetual ping by entering the key combo "CTRL+C" and pressing Enter.              



<img width="589" alt="Step 8" src="https://github.com/CGLuissi/configure-ad/assets/143234913/5c8d4218-7489-453a-a046-3903b77c8292">


<img width="571" alt="Step 8 1" src="https://github.com/CGLuissi/configure-ad/assets/143234913/86631eb0-9324-423a-8bdb-a8f6304f5db0">



 
8.) We will now install Active Directory through the server manager in DC-1. Click "add roles and features" then select "Add Active Directory Domain Services" then "add features" and click "next" until you get to the screen showing all the active directory services being installed. Install and wait for it to complete, then go back to the server manager page. Click the flag with the exclamation point, then promote the server to a domain controller. Active Directory is now up and running, and we can begin to configure user and object settings. We can begin by creating an organizational forest for all our users. Select "Add a new forest" and then type in a domain name (this can be anything you'd like). Create a DSRM password and click next until you reach the NETBIOS domain name; let the system create a domain name and click next until you reach the pre-requisite check then install. With the creation of active directory and the domain name, our VM will prompt a restart and reconnection. Head back to the azure services page and look at the DC-1 public ip, as it may have changed with the restart.  NOTE: If you can't proceed past the DNS Options prompt, make sure the checkbox is unchecked. 
 
 
</p>
<br />

<img width="292" alt="Step 9" src="https://github.com/CGLuissi/configure-ad/assets/143234913/d99ef86d-938f-4b42-86c1-d4421eb11d2b">




9.) Attempt to log back on to the DC-1 VM and observe what happens; you may have trouble signing in because the VM has officially become a domain controller and is now looking for a slightly different username in order to log in. The server is now looking for a username within the context of a domain name, meaning that you now have to clarify that you're signing specifically into the created domain with your username. For example, if your Username was "labuser" and your selected domain name was "mydomain.com", then your new login info must be "mydomain.com\labuser". Open up Remote Desktop then select "show options" and select your IP, then enter mydomain.com\labuser.


<img width="415" alt="Step 10" src="https://github.com/CGLuissi/configure-ad/assets/143234913/79ca7405-6de8-4088-9473-5879180d6ac1">



10.) Now that you are signed back into DC-1, click on the start menu and search for Active Directory Users and Computers. On the left-hand side, select your domain name then right click ->New -> Organaizational Unit. Name the unit "_EMPLOYEES", and make another unit named "_ADMINS". Now click then right click "_ADMINS" and create a new User. Name the user Jane Doe with the logon name "jane_admin" and set a password that you will remember. Make sure to uncheck the box that says "User must change password at next logon" at the next screen. Next, give Jane Doe access to the domain admin security group by right clicking the name, and selecting Properties -> "Member Of" -> type in Domain Admins. Click "Check Names" then click ok -> apply -> ok.


<img width="281" alt="Step 11" src="https://github.com/CGLuissi/configure-ad/assets/143234913/b89c771c-2197-4bdc-bc34-95042fd833d5">



11.) As an experiment, open up command prompt and type in and enter "hostname"; now type the command "whoami". These two commands show you the host name of your current system and clarify which user is currently in access, respectively. Enter in the command "logoff" and restart the VM, but this time select show options and sign in as "mydomain.com\jane_admin" with your chosen password. 


<img width="424" alt="STEP13 Rv" src="https://github.com/CGLuissi/configure-ad/assets/143234913/38144791-d90d-4091-961a-b0dfb6ace963">



12.) In Client-1, right click Start, and go to System ->  Settings -> About -> Rename this PC (advanced). Click Change and then select Domain; enter mydomain.com and observe that the connection can't be made. This is because the DNS settings for Client-1 are on a public IP, and not connected directly to DC-1. You can check this yourself by opening up command prompt and typing this command: "ipconfig/all". In order to actually join the DNS server as Client-1, we are going to set Client-1's DNS address as the private IP for DC-1. In the azure portal get the private IP for DC-1, then go to Client-1's Networking tab and select its network interface. Now select the DNS servers tab and select custom. Enter the private IP for DC-1 and click Save. Client-1 will need to be restarted for the setting to save, so go back to the Resources tab, select Client-1 and click the restart option. 



<img width="784" alt="STEP 13" src="https://github.com/CGLuissi/configure-ad/assets/143234913/0bdf6422-e601-41c6-8c94-027f37657a64">



13.) Reconnect to Client-1 as labuser, and enter the "ipconfig/all" command in command prompt. Our DNS server is now almost connected, but we can finalize this by right clicking the start menu -> system -> rename this pc (advanced) -> change -> domain. When prompted for a username and password, sign as "mydomain.com/jane_admin" using your chosen passsword. When this goes through, you will be prompted to restart your computer, so reload the VM and sign as mydomain.com\jane_admin. Once back in, right click the start menu and follow these steps: settings -> search "remote desktop" -> select users that remotely access this PC -> add "domain users". By doing this, we should be able to log back into our domain as any user, and we will test this in the next step.


14.) Switch back over to DC-1 and make sure you are signed in as jane_admin; if not, enter the logoff command in command prompt and sign back in. Open up the Powershell ISE application and run as an administrator. Copy this {script}(https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)














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
