<p align="center">
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
Setup Resources in Azure

 - Create the Domain Controller VM (Windows Server 2022) named “DC-1”
 - Set Domain Controller’s NIC Private IP address to be static
 
 - Create the Client VM (Windows 10) name
 Ensure that both VMs are in the same Vnet 
 
 Ensure Connectivity between the client and Domain Controller
 
 - Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> 
  
 - Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
  
 - Check back at Client-1 to see the ping succeed

  
Install Active Directory
 - Login to DC-1 and install Active Directory Domain Services
 - Promote as a DC: Setup a new forest as mydomain.com
 - Restart and then log back into DC-1 as user: mydomain.com\(whatever name created)
  
  Create an Admin and Normal User Account in AD
 - In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
 - Create a new OU named “_ADMINS”
 - Create a new employee named 
 - Add name_admin to the “Domain Admins” Security Group
 - Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\name_admin”
 - User name_admin as your admin account from now on

  Join Client-1 to your domain (mydomain.com)
 - From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
 - From the Azure Portal, restart Client-1
 - Login to Client-1 (Remote Desktop) as the original local admin and join it to the domain (computer will restart)
 - Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
 - Create a new OU named “_CLIENTS” and drag Client-1 into there

  Setup Remote Desktop for non-administrative users on Client-1
 - Log into Client-1 as mydomain.com\name_admin and open system properties
 - Click “Remote Desktop”
 - Allow “domain users” access to remote desktop
 - log into Client-1 as a normal, non-administrative user now
  
  Create many users and attempt to log into client-1 with one of the users
 - Login to DC-1 as name_admin
 - Open PowerShell_ise as an administrator
 - Run A script and observe the accounts being created
 - Open ADUC and observe the accounts in the appropriate OU
 - attempt to log into Client-1 with one of the accounts 



  
  


