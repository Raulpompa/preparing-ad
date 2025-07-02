<p align="center">
<img src="https://i.imgur.com/p81C8rU.jpeg" alt="ad logo"/>
</p>

<h1>Preparing Active Directory</h1>
<p>When preparing Active Directory (AD), I will create two VMs (Virtual Machines). One of the VMs will run a Windows Server to act as a Domain controller. The second VM will act as a client running Windows 10 to join the domain. In the upcoming projects, I will launch AD and run a script using PowerShell to create users in the domain. From there, I'll be able to log into the client VM and manage the accounts, as well as update group policies. Doing this will create a real-life Active Directory environment.  </p>

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
  <p></p>
<img src="" alt="osTicket Lifecycle"/>
</p>
<p>
  <p></p> 
<img src="" alt="osTicket Lifecycle"/>
</p>
<p>
  <p></p>
<img src=""  alt="osTicket Lifecycle"/>
</p>
<p>
  <p></p>
<img src="" alt="osTicket Lifecycle"/>
</p>
<p>
  <p></p> 
<img src="" alt="osTicket Lifecycle"/>
</p>
<p>
  <p></p>
<img src=""  alt="osTicket Lifecycle"/>
</p>
<p>
  <p></p>
<img src="" alt="osTicket Lifecycle"/>
</p>
<p>
  <p></p> 
<img src="" alt="osTicket Lifecycle"/>
</p>
<p>
  <p></p>
<img src=""  alt="osTicket Lifecycle"/>
</p>
