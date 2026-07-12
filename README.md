<h1>Active Directory Home-Lab</h1>

<h2>Description</h2>
A personal project, that throughly goes over the setup of establishing a virtualized networking environment with the use of Orcale VirtualBox to create VMs (Virtual Machines) such as the DC (Domain Controller) utilizing Windows Server 2019 and a Windows 10 VM on a simulated coporate environment. This project will also incorporate how to set up server roles for Active Directory Domain Service (AD DS), Remote Access Server/Network Address Translation (RAS/NAT), and DHCP (Dynamic Host Configuration Protocol) with DHCP scope. The project will also contain a PowerShell script to add over 1,000 users onto the coporate netowork, to simulate how multiple users will engage with the network to gain access. The project will showcase the configuration of creating a Windows 10 VM with an Internal (NIC), as well using Active Directory to access CLIENT1 PC (Windows 10 VM). 
<br />


<h2>Programs and Utilities Used</h2>

- <b>Oracle VirtualBox</b>
- <b>Windows 2019 Server</b>
- <b>Windows 10 Pro</b>
- <b>PowerShell</b>

<h2>Overview of Network Topology Diagram</h2>


<p align= "center">
<img src="https://i.imgur.com/u5kitXP.png" height=80% width=80%/>
<br />
<p align= "left">
<b>The picture above depicts a general diagram that showcases the entire home-lab network structure. The DC (Domain Controller), consists of two NICs (Network Interface Cards). One NIC will be configured for forwarding/receiving data traffic to the Internet, and will be repsectively named "INTERNET". The IP configuration for the "INTERNET" NIC will be obtained by the home router (In this use case for the lab it will come from my own personal home router). The other NIC will be configured to forwarding/receiving data traffic in the internal network environment, and will be respectively named "INTERNAL". The IP configuration for the "INTERNAL" NIC will be manually assigned, as indicated by the diagram. The DC will be installed with Windows 2019 Server, this will allow additional configurations to be installed and provide as the main point of entry for internal users on the network to circulate traffic within the environment, as well send/receive traffic to the Internet. Within the DC, the following configurations will be installed Active Directory Domain Service (AD DS), Remote Access Server/Network Address Translation (RAS/NAT), and Dynamic Host Configuration Protocol (DHCP). With AD DS installed, it allows the implementation of a FQDN (Fully Qualified Domain Name), and in the use case for this home lab it will be named mydomain.com. With RAS/NAT, it will allow routing of clients data on the private internal network to communicate with the DC to reach the Internet. DHCP configurations will also be installed, and will provide a way to automatically assign IPv4 addresses to client devices, and in this use case it will be for CLIENT1 VM. The CLIENT1 VM will be installed with Windows 10 Pro, with the additional feature of having its own NIC that will be named INTERNAL. IP configuration will be obtained from the DC through DHCP. This will enable the VM to connect to the VMware Network to the internal NIC of the DC.</b>
