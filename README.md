<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
In this home lab, I will install Active Directory Domain Services, set up a forest as mydomain.com, and use Active Directory Users and Computers (ADUC) to create and assign users to connect to VM-Client-1 via Remote Desktop (RDP). I will also be using Powershell ISE to run a script that creates randomized users to be able to connect to client-1.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

Part 1
Install Active Directory
—
Login to DC-1 and install Active Directory Domain Services

 ![image](https://github.com/user-attachments/assets/bfd0079c-3d85-4696-9537-d63fad2596cc)


Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)

![image](https://github.com/user-attachments/assets/79352e0e-f5d7-42cd-b4b4-cbfb84ee0230)

Restart and then log back into DC-1 as user: mydomain.com\labuser

Create a Domain Admin user within the domain
—
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called 
“_EMPLOYEES”

Create a new OU named “_ADMINS”

 ![image](https://github.com/user-attachments/assets/d379e361-fbd5-41ce-b3cd-c3f23740291b)


Create a new employee named “Jane Doe” (same password) with the username of “jane_admin” / Cyberlab123!

Add jane_admin to the “Domain Admins” Security Group

Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin”

User jane_admin as your admin account from now on


Join Client-1 to your domain (mydomain.com)

Login to Client-1 as the original local admin (labuser) and join it to the domain (computer will restart)

Login to the Domain Controller and verify Client-1 shows up in ADUC

Create a new OU named “_CLIENTS” and drag Client-1 into there

![image](https://github.com/user-attachments/assets/08d3fa62-dace-4b14-9286-f87454232184)
 

Part 2

Setup Remote Desktop for non-administrative users on Client-1

Log into Client-1 as mydomain.com\jane_admin


Open system properties

Click “Remote Desktop”

Allow “domain users” access to remote desktop

You can now log into Client-1 as a normal, non-administrative user now

 ![image](https://github.com/user-attachments/assets/b5796d06-cfbd-4e40-a09e-08034bf7f68b)



Create a bunch of additional users and attempt to log into client-1 with one of the users

Login to DC-1 as jane_admin

Open PowerShell_ise as an administrator

Create a new File and paste the contents of the script into it

Run the script and observe the accounts being created

 ![image](https://github.com/user-attachments/assets/54e8f607-4f7b-407c-84e2-adce0f33bb04)


