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

- Creation of our resources 
- Observe ICMP Traffic
- Observe SSH, DHCP, DNS, and RDP traffic


<h2>Actions and Observations</h2>

<h3>Part 1 (Create our Resources></h3>
<p>
  <ol>
    <li>Create a Resource Group:</li>
    <ul>
      <li>Log in to your Azure portal.</li>
      <li>Navigate to the Resource Groups section.</li>
      <li>Click on "Create Resource Group" and provide necessary details like name, region, etc.</li>
    </ul>
<img src="https://i.imgur.com/iF3W4gb.png" height="80%" width="80%" alt="Create a Resource Group"/>
</p>


<p>
  <li>Create a Windows 10 Virtual Machine (VM):</li>
  <ul>
    <li>In the Azure portal, navigate to Virtual Machines.</li>
    <li>Click on "Add" to create a new VM.</li>
    <li>During VM creation, select the previously created Resource Group.</li>
    <li>Allow it to create a new Virtual Network (Vnet) and Subnet.</li>
  </ul>
<img src="https://i.imgur.com/QzoV88n.png" height="60%" width="60%" alt="Virtual Machine"/>
</p>


<p>
  <li>Create a Linux (Ubuntu) VM:</li>
  <ul>
    <li>Repeat the process for creating a VM.</li>
    <li>During VM creation, select the previously created Resource Group and Vnet.</li>
  </ul>
<img src="https://i.imgur.com/10qOnQj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
  <li>Observe Your Virtual Network within Network Watcher:</li>
  <ul>
    <li>Navigate to Network Watcher in the Azure portal.</li>
    <li>Observe the virtual network you've created to ensure it's set up correctly.</li>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</ol>
<br />

<h2>Part 2 (Observe ICMP Traffic)</h2>

<ol>
<p>
  <li>Connect to Windows 10 VM and Install Wireshark:</li>
  <ul>
    <li>Use Remote Desktop to connect to your Windows 10 Virtual Machine.</li>
    <ul>
      <li>In the Azure Portal, navigate to the Virtual Machines section, select VM1, and then copy its public IP address.</li>
      <li>Go to the Start menu, search for "Remote Desktop," paste the public IP address into the appropriate field, and enter the login credentials.</li>
      <img src="https://i.imgur.com/pl0YhL7.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
      <img src="https://i.imgur.com/7hk7aT5.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
      <img src="https://i.imgur.com/PuoouXG.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
    </ul>
    <li>Install Wireshark within the VM.</li>
  <ul>
    <li>Go to https://www.wireshark.org/download.html and select the appropriate version for your operating system.</li>
  </ul>
  </ul>
<img src="https://i.imgur.com/XaJNLo2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
  <li>Filter and Observe ICMP Traffic:</li>
  <ul>
    <li>Open Wireshark and filter for ICMP traffic only.</li>
    <li>Retrieve the private IP address of the Ubuntu VM and ping it from within the Windows 10 VM.</li>
    <li>Observe ping requests and replies within Wireshark.</li>
    <img src="https://i.imgur.com/6KYTlVp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
    <li>Ping a public website from the Windows 10 VM and observe the traffic.</li>
    <ul>
    <li> Ping www.google.com</li>
      <img src="https://i.imgur.com/qWDNdZS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
    </ul>
    <li>Initiate perpetual/non-stop ping from Windows 10 VM to Ubuntu VM.</li>
    <img src="https://i.imgur.com/DajRANa.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
    <li>Disable incoming ICMP traffic in Network Security Group of Ubuntu VM and observe the changes.</li>
    <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
    <li>Re-enable ICMP traffic and observe.</li>
    <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</ol>
<br />


<h2>Part 3 (Observe SSH, DHCP, DNS, and RDP Traffic)</h2>
<ol>
<p>
  <li>Filter and Observe SSH Traffic:</li>
  <ul>
    <li>Filter for SSH traffic in Wireshark.</li>
    <li>SSH into the Ubuntu VM from Windows 10 VM.</li>
    <li>Type commands and observe SSH traffic.</li>
    <li>Exit SSH connection.</li>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
  <li>Filter and Observe DHCP Traffic:</li>
  <ul>
    <li>Filter for DHCP traffic in Wireshark.</li>
    <li>Attempt to renew IP address from Windows 10 VM and observe DHCP traffic.</li>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
  <li>Filter and Observe DNS Traffic:</li>
  <ul>
    <li>Filter for DNS traffic in Wireshark.</li>
    <li>Use nslookup in Windows 10 VM to check IP addresses for google.com and disney.com.</li>
    <li>Observe DNS traffic.</li>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
  <li>Filter and Observe RDP Traffic:</li>
  <ul>
    <li>Filter for RDP traffic in Wireshark.</li>
    <li>Observe the traffic pattern and its continuous transmission.</li>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</ol>

