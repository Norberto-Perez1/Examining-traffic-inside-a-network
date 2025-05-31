<p align="center">
<img src="!(https://github.com/user-attachments/assets/1c465d4f-177f-46c2-89aa-747250b31734)
" alt="(https://github.com/user-attachments/assets/cd1ffdce-2ee4-47a2-bc70-49add6d0a79b)
"/>
</p>

<h1>Examining traffic inside a network</h1>
This tutorial outlines the implementation of a network protocol analyzer(Wireshark) to examine traffic between Azure virtual machines on the same virtual network.<br />

![Examining traffic inside a network](https://github.com/user-attachments/assets/3a12e9c8-eb5a-4a6b-bfd0-a5ceced03995)


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute/Firewall)
- Remote Desktop
- Wireshark
- PowerShell

<h2>Operating Systems Used </h2>

- Linux (Ubuntu)
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Create virtual machines in Azure
- Step 2: Set-up Wireshark inside Windows 10 virtual machine
- Step 3: Configure a Firewall(Network Security Group)
- Step 4: Observe traffic from different sources
- Step 5: Delete Resource Group
  
<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Start by creating a resource group inside of the Azure portal. To do this simply search for "Resource group" in the search bar at the top of the screen and once you have clicked on it, go over to "create" and click on that too. Set a name and Location and click on "Review + create" then click on "Create". The names used for resources in this lab are not obligatory but are created to be easy to read and to match their respective resource acourdingly.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
With the virtual machines ready to go now we'll need a way to access them, for this lab we'll be using Microsoft Remote Desktop.
To use it on a Windows computer you will just need to search for it on the searchbar located on the bottom left corner of your desktop and clicking on it once you have found it. In the case that you are using a Mac computer go to the apple menu then navigate to App Store and search for it there, install the app once you have found it.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now that we have Microsoft Remote Desktop we can connect to the virtual machines by inserting their public IP address then clicking connect and inserting the previosly created username and password, to find your windows-vm public IP address search for "Virtual Machines" inside of the Azure portal and look at the corresponding IP address below the "Public IP adress" column
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once inside of the windows-vm go to "Microsoft Edge" and search for "https://www.wireshark.org" using the searchbar. Now just click on download 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once inside of the windows-vm go to "Microsoft Edge" and search for "https://www.wireshark.org" using the searchbar. Now just click on download 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut 
</p>
<br />
