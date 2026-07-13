<h1 align="center">Active Directory Home-Lab</h1>

<h2>Description</h2>
A personal project, that throughly goes over the setup of establishing a virtualized networking environment with the use of Orcale VirtualBox to create VMs (Virtual Machines) such as the DC (Domain Controller) utilizing Windows Server 2019 and a Windows 10 VM on a simulated coporate environment. This project will also incorporate how to set up server roles for Active Directory Domain Service (AD DS), Remote Access Server/Network Address Translation (RAS/NAT), and DHCP (Dynamic Host Configuration Protocol) with DHCP scope. The project will also contain a PowerShell script to add over 1,000 users onto the coporate netowork, to simulate how multiple users will engage with the network to gain access. The project will showcase the configuration of creating a Windows 10 VM with an Internal (NIC), as well using Active Directory to access CLIENT1 PC (Windows 10 VM). 
<br />


<h2>Programs and Utilities Used</h2>

- <b>Oracle VirtualBox</b>
- <b>Windows 2019 Server</b>
- <b>Windows 10 Pro</b>
- <b>PowerShell</b>

<h2 align="center">Overview of Network Topology Diagram</h2>


<p align= "center">
<img src="https://i.imgur.com/jz6XKou.png" height=80% width=80%/>
<br />
<p align= "left">
<b>The picture above depicts a general diagram that showcases the entire home-lab network structure. The DC (Domain Controller), consists of two NICs (Network Interface Cards). One NIC will be configured for forwarding/receiving data traffic to the Internet, and will be repsectively named "INTERNET". The IP configuration for the "INTERNET" NIC will be obtained by the home router (In this use case for the lab it will come from my own personal home router). The other NIC will be configured to forwarding/receiving data traffic in the internal network environment, and will be respectively named "INTERNAL". The IP configuration for the "INTERNAL" NIC will be manually assigned, as indicated by the diagram. The DC will be installed with Windows 2019 Server, this will allow additional configurations to be installed and provide as the main point of entry for internal users on the network to circulate traffic within the environment, as well send/receive traffic to the Internet. Within the DC, the following configurations will be installed Active Directory Domain Service (AD DS), Remote Access Server/Network Address Translation (RAS/NAT), and Dynamic Host Configuration Protocol (DHCP). With AD DS installed, it allows the implementation of a FQDN (Fully Qualified Domain Name), and in the use case for this home lab it will be named mydomain.com. With RAS/NAT, it will allow routing of clients data on the private internal network to communicate with the DC to reach the Internet. DHCP configurations will also be installed, and will provide a way to automatically assign IPv4 addresses to client devices, and in this use case it will be for CLIENT1 VM. The CLIENT1 VM will be installed with Windows 10 Pro, with the additional feature of having its own NIC that will be named INTERNAL. IP configuration will be obtained from the DC through DHCP. This will enable the VM to connect to the VMware Network to the internal NIC of the DC.</b>
<br />

<h2 align="center">Base Configuration of Domain Controller (DC) Windows 2019 Server VM</h2>


<p align= "center">
<img src="https://i.imgur.com/1TWaWX0.png" height=80% width=80%/>
<br />
<p align= "left">
<b>This is the baseline configuration for the setup of the DC server in Orcale VirtualBox. Two NICs will be enabled for this specific server, as indicated underneath the "Network" tab for the configuration window. Some additional parameters that can be manually configured are core processors (dependent on the actual core threads of one's computer), and base memory (in this lab example I've chosen 2,048MB = 2GB).</b>
<br />
  
<h2 align="center">IP Addressing for Internet & Internal Network</h2>
<p align="center">
  <img src="https://i.imgur.com/vBakRje.png" width="32%">
  <img src="https://i.imgur.com/pV4rYfK.png" width="32%">
  <img src="https://i.imgur.com/Bo6neNV.png" width=32%>
</p>
<br />
<p align="left">
<b>Two network adapters are installed in the DC Virtual Machine. Ethernet Adapter 1 Status indicates a APIPA address assigned to it, indicated by the 169.254.116.165 address. This means the network adapter was not able to obtain an IP address from the DHCP Server. And will serve to be the INTERNAL NIC. Ethernet Adapter 2 has an IP address of 10.0.2.15, which indicates that it obtained an IP address from the home router. This will serve to be the INTERNET NIC.</b>
<br />
<p align="center">
  <img src="https://i.imgur.com/UmD71eP.png" width=32%>
  <img src="https://i.imgur.com/Wu9PtCq.png" width=32%>
  <img src="https://i.imgur.com/qFGTQtr.png" width=32%>
</p>
<p align="left">
<b>After validating each IP address, rename each network adapter to its respective name for easier clarification in future configuration options. As well, renaming the PC to DC (Domain Controller), as this computer will serve as the main server for hosting various server roles</b>
<br />

<h2 align="center">Configuring Active Directory Domain Service on Domain Controller</h2>
<p align="center">
  <img src="https://i.imgur.com/fmz9uiX.png" width=32%>
  <img src="https://i.imgur.com/am3fPiQ.png" width=32%>
  <img src="https://i.imgur.com/YxDVztZ.png" width=32%>
</p>
<br />
<p align="center">
  <img src="https://i.imgur.com/3yiDSr9.png" width=32%>
  <img src="https://i.imgur.com/X6VUIxm.png" width=32%>
  <img src="https://i.imgur.com/hRv4h2s.png" width=32%>
</p>
<br />
<p align="center">
  <img src="https://i.imgur.com/7lBBWj7.png" width=32%>
  <img src="https://i.imgur.com/nEkHWxS.png" width=32%>
</p>
<p align="left">
<b>The screenshots above showcase the necessary steps to configuration and deployment configuration for Active Directory Domain Services (AD DS) onto the Domain Controller (DC) as a server role. If everything is configured and installed correctly, the log-in page should display the domain name.</b>
<br />

<h2 align="center">Creating a dedicated Admin Controller Account</h2>
<p align="center">
  <img src="https://i.imgur.com/cO8r8E8.png" width=32%>
  <img src="https://i.imgur.com/dyqR6Zw.png" width=32%>
  <img src="https://i.imgur.com/RgNvwlo.png" width=32%>
</p>
<br />
<p align="center">
  <img src="https://i.imgur.com/41Mojik.png" width=32%>
  <img src="https://i.imgur.com/hwyLvfE.png" width=32%>
  <img src="https://i.imgur.com/k73rvzq.png" width=32%>
</p>
<p align="left">
<b>The screenshots go through the configuration process of creating a dedicated admin controller account. The purpose of this, is to isolate highly privileged rights from the user's standard, daily-use profile. It is best practice that severely limits the scope of an attack and protect critical infrastructure like Active Directory Domain Service, from malware or credential theft. If the configuration process is successful, you will be able to log in with the adminstrator credentials through the VM, as indicated by the last screenshot.</b>
<br />

<h2 align="center">Installing RAS/NAT (Remote Access Server) (Network Address Translation)</h2>
<p align="center">
  <img src="https://i.imgur.com/s5G7BSX.png" width=32%>
  <img src="https://i.imgur.com/nmB9PVO.png" width=32%>
  <img src="https://i.imgur.com/hXJEeJD.png" width=32%>
</p>
<br />
<p align="center">
  <img src="https://i.imgur.com/vIfIpxb.png" width=32%>
  <img src="https://i.imgur.com/aLQwZG6.png" width=32%>
  <img src="https://i.imgur.com/nPjV0gd.png" width=32%>
</p>
<p align="left">
<b>The configuration of RAS/NAT allow a server to function as a software-based router and gateway for data traffic that flows through the network. Remote Access Service, enables remote clients to securely connect to the coporate environment, while allowing multiple private devices with their own private IP address to share a single public IP address for internet access through Network Address Translation.</b>
<br />
  
<h2 align="center">Installing and Setting up Dynamic Host Configuration Protocol (DHCP)</h2>
<p align="center">
  <img src="https://i.imgur.com/1Bt1zRS.png" width=32%>
  <img src="https://i.imgur.com/byz8l8U.png" width=32%>
  <img src="https://i.imgur.com/1dulMv9.png" width=32%>
</p>
<br />
<p align="center">
  <img src="https://i.imgur.com/sM53I3m.png" width=32%>
  <img src="https://i.imgur.com/m3djXoa.png" width=32%>
  <img src="https://i.imgur.com/bJCndzj.png" width=32%>
</p>
<br /> 
<p align="center">
  <img src="https://i.imgur.com/2zGAiE6.png" width=32%>
  <img src="https://i.imgur.com/QNLTryu.png" width=32%>
</p>
<p align="left">
<b>The screenshots above show the configuration and installation of DHCP server role on the DC server. DHCP allows the automatic assignment of IP address to the network, as they join it without the need to manually configure it for each device. The DHCP scope for this lab is set to 172.16.0.100-172.16.0.200, giving about 101 usable dynamic IP addresses for the network clients. The default gateway and DNS will be set to 172.16.0.1, which is the IP address of the INTERNAL NIC of the DC server. This is done because all data traffic and queries will be handled by the DC. If all configurations are set properly, the link status of the IPv4 address should be a green arrow pointing up, which indicates that everything is working properly</b>
















