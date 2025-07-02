<p align="center">
<img src="https://i.imgur.com/p81C8rU.jpeg" alt="ad logo"/>
</p>

<h1>Preparing Active Directory</h1>
<p>When preparing Active Directory (AD), I will create two VMs (Virtual Machines). One of the VMs will run a Windows Server to act as a Domain controller. The second VM will act as a client running Windows 10 to join the domain. In the upcoming projects, I will launch AD and run a PowerShell script to create users in the domain. From there, I'll be able to log into the client VM and manage the accounts, as well as update group policies. Doing this will create a real-life Active Directory environment.  </p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Virtual Machines
- Remote Desktop Connection
<h2>Operating Systems Used</h2>

- Windows Server
- Windows 10
<h2>Project Step-By-Step</h2>

<p>
  <p>Begin by creating a resource group in Microsoft Azure.</p>
<img src="https://i.imgur.com/31n21R5.png" alt="resource group"/>
</p>
<p>
  <p>Next, create a virtual network as follows.</p> 
<img src="https://i.imgur.com/OxgNdLg.png" alt="virtual network"/>
</p>
<p>
  <p>Once the resource group and virtual network are created, I’ll create and set up the virtual machine that will serve as our Domain Controller. Be sure to use a Windows Server image.</p>
<img src="https://i.imgur.com/vgIk9aP.png"  alt="domain controller"/>
</p> 
<p>
  <p></p>
<img src="https://i.imgur.com/BXA1xet.png" alt="VM"/>
</p>
<p>
  <p>In the Networking tab of this VM, I’ll ensure it is created within the virtual network I just set up. I’ll leave all other settings at their defaults and proceed to create the VM.</p> 
<img src="https://i.imgur.com/LZlWvSA.png" alt="within virtual network"/>
</p>
<p>
  <p>Next, I’ll set up a second virtual machine to act as the client. This time, make sure to select a Windows 10 image, rather than the Windows Server image used for the Domain Controller.</p>
<img src="https://i.imgur.com/GSzaVR6.png"  alt="client vm"/>
</p>
<p>
  <p></p>
<img src="https://i.imgur.com/SyMRidQ.png" alt="client vm"/>
</p>
<p>
  <p>In the Networking tab of this VM, I’ll ensure it’s connected to the same virtual network as the previously created machine. I’ll leave all other settings at their defaults and then create the VM.</p> 
<img src="https://i.imgur.com/fTdmmcT.png" alt="networking tab c-1 vm"/>
</p>
<p>
  <p>Since the Domain Controller (DC) will also serve as our DNS server, I need to ensure its private IP address doesn’t change. By default, Azure sets the IP to dynamic, but for reliability, I’ll change it to static. This way, when I configure the client to use the DC for DNS, it won't lose connection due to an unexpected IP change. To do this, I’ll access the DC’s network settings and update the IP allocation to static.</p>
<img src="https://i.imgur.com/SSVc7zF.png"  alt="static IP"/>
</p>
<p>
  <p></p>
<img src="https://i.imgur.com/GGHe4YF.png" alt="staic IP DC 1"/>
</p>
<p>
  <p>Now, I’ll connect to the Domain Controller via Remote Desktop using its public IP and the username and password I created when configuring the VM.</p> 
<img src="https://i.imgur.com/lPmsseN.png" alt="connecting to DC-1"/>
</p>
<p>
  <p>After logging in, you should see the Server Manager window by default. If you’re seeing a standard Windows desktop instead, it’s possible you connected to the client VM or chose the wrong image during the Domain Controller setup.</p>
<img src="https://i.imgur.com/BdpMGF6.png"  alt="server manager window"/>
</p>
<p>
  <p>For the sake of this lab, I’ll disable the firewall — something you typically wouldn’t do in a production environment. To begin, I’ll right-click the Start button, open the Run dialog, and enter wf.msc to access the firewall settings.</p>
<img src="https://i.imgur.com/AelS2Mg.png" alt="disable firewall"/>
</p>
<p>
  <p>Open Windows Defender Firewall Properties, and under each tab — Domain Profile, Private Profile, and Public Profile — switch the firewall setting to Off</p> 
<img src="https://i.imgur.com/1GdnpiB.png" alt="disable firewall"/>
</p>
<p>
  <p></p>
<img src="https://i.imgur.com/VqZCNCx.png"  alt="firewall defender"/>
</p>
<p>
  <p></p>
<img src="https://i.imgur.com/PW3VFWW.png" alt="firewall defender"/>
</p>
<p>
  <p>At this point, all firewall settings should appear as disabled.</p> 
<img src="https://i.imgur.com/ABBdJS6.png" alt="disabled firewall"/>
</p>
<p>
  <p>Now, I’ll set the client’s DNS to use the Domain Controller. First, I’ll go back to Azure and copy the private IP address of the DC.</p>
<img src="https://i.imgur.com/1NfaFCI.png"  alt="clients DNS to DC-1"/>
</p>
<p>
  <p>Next, I’ll access the client VM’s network settings. I’ll select its NIC, go to the DNS Servers section under Settings, and change the configuration from Inherit from virtual network to Custom. Then, I’ll input the Domain Controller’s private IP address and save.</p>
<img src="https://i.imgur.com/s4EkJPx.png" alt="input DC-1's private IP into client-1"/>
</p>
<p>
  <p>Once the settings are saved, I’ll reboot the client VM to apply the new DNS configuration.</p> 
<img src="https://i.imgur.com/vkhp8fV.png" alt="restart VM"/>
</p>
<p>
  <p>After the reboot, I’ll connect to the client VM via Remote Desktop, using its public IP and the username and password I established when setting it up.</p>
<img src="https://i.imgur.com/Jrm1mHM.png"  alt="RDP connect client"/>
</p>
<p>
  <p>After logging in, I’ll launch PowerShell and use the ping command with the Domain Controller’s private IP to test connectivity. If the ping fails with a timeout error, verify that both VMs are connected to the same virtual network in Azure. If they aren’t, you’ll need to recreate the machines on the same network to resolve the issue.</p>
<img src="https://i.imgur.com/hzp66Nm.png" alt="ping dc-1 and verify both vm's are connected"/>
</p>
<p>
  <p>While connected, I’ll verify that the DNS configuration points to the Domain Controller by running ipconfig /all and checking the DNS Servers section. If configured properly, it will show the DC’s IP address.</p> 
<img src="https://i.imgur.com/rHjjW9B.png" alt="verify DNS configuration"/>
</p>
<p>
  <h2>The Active Directory infrastructure has been successfully set up!</h2>
  <p>Two virtual machines have been set up successfully: a Windows Server VM acting as the Domain Controller, and a Windows 10 VM serving as the client.

In upcoming projects, I’ll deploy Active Directory, automate user creation with scripts, enable client VM logins, and manage user accounts and group policies — all to replicate a real-world IT environment.</p>
