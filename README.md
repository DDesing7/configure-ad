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

<h2>High-Level Deployment and Configuration Steps</h2>

- Install Active Directory
- Create a Domain Admin user within the domain
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

Step 1: Install Active Directory
-
 - Login to DC-1 and install Active Directory Domain Services
 - Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
 - Restart and then log back into DC-1 as user: mydomain.com\labuser

Step 2: Create a Domain Admin user within the domain
-
 - In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
 - Create a new OU named “_ADMINS”
 - Create a new employee named “Jane Doe” (same password) with the username of “jane_admin” / Cyberlab123!
 - Add jane_admin to the “Domain Admins” Security Group
 - Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin”
 - User jane_admin as your admin account from now on

Step 3: Join Client-1 to your domain (mydomain.com)
-
 - Login to Client-1 as the original local admin (labuser) and join it to the domain (computer will restart)
 - Login to the Domain Controller and verify Client-1 shows up in ADUC
 - Create a new OU named “_CLIENTS” and drag Client-1 into there

Step 4: Setup Remote Desktop for non-administrative users on Client-1
-
 - Log into Client-1 as mydomain.com\jane_admin
 - Open system properties
 - Click “Remote Desktop”
 - Allow “domain users” access to remote desktop
 - You can now log into Client-1 as a normal, non-administrative user now

Step 5: Create a bunch of additional users and attempt to log into client-1 with one of the users
-
 - Login to DC-1 as jane_admin
 - Open PowerShell_ise as an administrator
 - Create a new File and paste the contents of the script into it
 - Run the script and observe the accounts being created
 - When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES)
 - attempt to log into Client-1 with one of the accounts (take note of the password in the script)
