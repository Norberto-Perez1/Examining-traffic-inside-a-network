
![Examining traffic inside a network](https://github.com/user-attachments/assets/3a12e9c8-eb5a-4a6b-bfd0-a5ceced03995)

<h1>Examining traffic inside a network</h1>
This tutorial outlines the implementation of a network protocol analyzer(Wireshark) to examine traffic between Azure virtual machines on the same virtual network.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Wireshark
- PowerShell

<h2>Operating Systems Used </h2>

- Linux (Ubuntu)
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Create virtual machines in Azure
- Step 2: Set-up Wireshark inside Windows 10 virtual machine
- Step 3: Observe traffic from different sources
- Step 4: Delete Resource Group

<h2>Deployment and Configuration Steps</h2>

![Resource group](https://github.com/user-attachments/assets/b6b52e77-d044-4d9a-ae2c-5d709f8ae9fd)

<p>
Start by creating a resource group inside of the Azure portal. To do this simply search for "Resource group" in the search bar at the top of the screen and once you have clicked on it, go over to "create" and click on that too. Set a name and Location and click on "Review + create" then click on "Create". The names used for resources in this lab are not obligatory but are created to be easy to read and to match their respective resource acourdingly.
</p>
<br />

<p>
Now we will create the First Virtual Machine, search for "Virtual machines" and create with the following specifications:
</p>

- name: windows-vm
- image: Windows 10 Pro, version 22H2 - x64 Gen2
- size: whatever you are comfortable with using(recommend at least 2 vcpus, 8 GiB memory for a smoother experience but not required)
- username: testuser
- password: Testuser123!
- Licensing: check box(if it applies to you)

<p>
After you have set those specifications you can click on "Review + create" then click on "Create". This will do two things , create the windows 10 pro virtual machine and automatically create a Virtual Network for the virtual machine named "windows-vm-vnet" or a variation of the this depending on what you named your virtual machine.
</p>

<br />

![Virtual Network](https://github.com/user-attachments/assets/6326aba8-561f-4568-998a-42fbb1fe3fff)
<p>
Create the second Virtual Machine by following the previous steps but use this specifications instead:
</p>

- name: linux-vm
- image: Ubuntu Server 22.04 LTS - x64 Gen2
- size: whatever you are comfortable with using(recommend at least 2 vcpus, 8 GiB memory for a smoother experience but not required)
- authentication type: Password
- username: testuser
- password: Testuser123!
- virtual network: windows-vm-vnet

<p>
After you have set those specifications before clicking "Review + create" click "Next: Disks", then "Next: Networking" and once you get to the Networking section make sure the virtual network assigned is the previosly created. After that is done you can finish creating the virtual machine.
</p>


<br />

![microsoft rdp](https://github.com/user-attachments/assets/ed3e0ba5-b48f-47c7-bc23-b7eae721dd57)
![Mac rdp](https://github.com/user-attachments/assets/26c6a1f3-0859-4fa4-a572-5cebe6d5736e)

<p>
With the virtual machines ready to go now we'll need a way to access them, for this lab we'll be using Microsoft Remote Desktop.
To use it on a Windows computer you will just need to search for it on the searchbar located on the bottom left corner of your desktop and clicking on it once you have found it. In the case that you are using a Mac computer go to the apple menu then navigate to App Store and search for it there, install the app once you have found it.
</p>
<br />

![rdp connect](https://github.com/user-attachments/assets/208051b6-88a6-47b2-b301-9bfc4fc64cce)

<p>
Now that we have Microsoft Remote Desktop we can connect to the virtual machines by inserting their public IP address then clicking connect and inserting the previosly created username and password, to find your windows-vm public IP address search for "Virtual Machines" inside of the Azure portal and look at the corresponding IP address below the "Public IP adress" column
<br />

![Screenshot 2025-05-31 222235](https://github.com/user-attachments/assets/d16fe749-b894-4f2e-80da-7295ecbc64b6)

<p>
Once inside of the windows-vm go to "Microsoft Edge" and search for "https://www.wireshark.org" using the searchbar. Now just click on download and choose "Windows x64 Installer", after the file has been installed go to the top right of the website and click on open file to set up the installation for Wireshark. A pop up from User Account Control might appear, just click "Yes", now we just need to finish the set up for the installation, click on this options as they appear: Next>, Noted>, Next>, Next>, Next>, Next>, Next>, Install, I Agree, Install, Next>, Finish, Next>, Finish, Next>, Finish. If you find this a bit confusing just keep in mind that we don't make any changes to the default installation so you can just press next, noted, I agree, install, or finished until you are done with the installation.
</p>
<br />

![Ethernet port wireshark](https://github.com/user-attachments/assets/520caf2d-1b1c-4f8a-b9d5-14948a0c56fb)

<p>
With Wireshark now instaled search for it with the searchbar in your desktop and open the app. Inside of the app we can now filter for traffic in the filter searchbar, for the purpuse of this lab we will be filtering for two types of traffic, ICMP and RDP traffic inside of the Network port. Select the Ethernet port to view traffic passing throuh then Type "icmp" on the filter searchbar and select it. As of now you will not see any traffic but we will change that in the next step.
</p>
<br />

![linux private ip address](https://github.com/user-attachments/assets/77e7192f-92b4-482c-ad9e-df3ba5e1ee64)
![ping and traffic](https://github.com/user-attachments/assets/33330ea1-2078-4b55-bb26-5e058ee564ca)

<p>
In this step we will try to ping the linux-vm from our microsoft-vm using powershell and observe the traffic created inside of the icmp filter. To be able to ping the linux-vm we will need it's private IP, this can be found by going to Virtual Machines inside of the azure portal and selecting the linux-vm. Search and open "Windows PowerShell", once you are inside type "ping 10.0.0.5"(in this case 10.0.0.5 is the private IP address otherwise type the one you copied instead) and hit enter. Now traffic has appeared showing request from the windows-vm and replies from the linux-vm.
</p>
<br />

![rdp traffic](https://github.com/user-attachments/assets/448bd3d5-d5ca-45ec-a908-c4462c7bb7e5)

<p>
Try filtering for RDP traffic now and observe how traffic is constantly comming in, this is becauese the connection made with RDP is constantly sending information back and forth to be maintained.
</p>
<br />

![delete resource group](https://github.com/user-attachments/assets/5fac3fda-9232-484a-83ff-14071a853970)

<p>
This concludes the lab but I'll help you clean up before you go. We have 2 resource groups, 1 virtual network , and 2 virtual machines running. To eliminate all those resources we will head back to the Azure portal and then to resource groups, click on the "RG-Network-Activities" and once inside click on "delete resource group" and copy and paste the name were it asks you to (make sure to check the box to apply force delete on selected virtual machines). Repeart the same process for "NetworkWatcherRG" and you are done.
</p>
<br />
