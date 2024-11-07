<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
In this home lab, I will install Active Directory Domain Services (AD DS), set up a forest (`mydomain.com`), and use Active Directory Users and Computers (ADUC) to create and assign users to connect to `VM-Client-1` via Remote Desktop (RDP). I will also use PowerShell ISE to run a script that creates randomized users for RDP access.

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Remote Desktop</li>
  <li>Active Directory Domain Services</li>
  <li>PowerShell</li>
</ul>

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows Server 2022</li>
  <li>Windows 10 (21H2)</li>
</ul>

<h2>High-Level Deployment and Configuration Steps</h2>

<h3>Part 1: Install Active Directory</h3>
<ol>
  <li>Login to DC-1 and install Active Directory Domain Services</li>
  <p align="center">
    <img src="https://github.com/user-attachments/assets/bfd0079c-3d85-4696-9537-d63fad2596cc" alt="AD Installation Screenshot" />
  </p>

  <li>Promote the server as a Domain Controller and set up a new forest as <code>mydomain.com</code></li>
  <p align="center">
    <img src="https://github.com/user-attachments/assets/79352e0e-f5d7-42cd-b4b4-cbfb84ee0230" alt="Promote Domain Controller Screenshot" />
  </p>

  <li>Restart the server and log in as <code>mydomain.com\labuser</code></li>
  <li>Create Organizational Units (OUs) named <code>_EMPLOYEES</code> and <code>_ADMINS</code></li>
  <p align="center">
    <img src="https://github.com/user-attachments/assets/d379e361-fbd5-41ce-b3cd-c3f23740291b" alt="ADUC Organizational Units Screenshot" />
  </p>

  <li>Create a Domain Admin user (<code>jane_admin</code>) in ADUC and add her to the <code>Domain Admins</code> security group</li>
  <li>Log in as <code>mydomain.com\jane_admin</code> for administrative tasks</li>
</ol>

<h3>Join Client-1 to the Domain</h3>
<ol>
  <li>Login to Client-1 as the local admin and join it to the domain <code>mydomain.com</code></li>
  <li>Verify Client-1 appears in ADUC</li>
  <p align="center">
    <img src="https://github.com/user-attachments/assets/08d3fa62-dace-4b14-9286-f87454232184" alt="Client-1 in ADUC Screenshot" />
  </p>

  <li>Create a new OU named <code>_CLIENTS</code> and move Client-1 into it</li>
</ol>

<h3>Part 2: Setup Remote Desktop for Non-Administrative Users</h3>
<ol>
  <li>Log in to Client-1 as <code>mydomain.com\jane_admin</code></li>
  <li>Enable Remote Desktop and allow access for domain users</li>
  <p align="center">
    <img src="https://github.com/user-attachments/assets/b5796d06-cfbd-4e40-a09e-08034bf7f68b" alt="Remote Desktop Setup Screenshot" />
  </p>

  <li>Test by logging in as a non-administrative user</li>
</ol>

<h3>Create Randomized Users with PowerShell</h3>
<ol>
  <li>Login to DC-1 as <code>jane_admin</code></li>
  <li>Open PowerShell ISE as an administrator</li>
  <li>Run a PowerShell script to create multiple users for RDP access</li>
  <p align="center">
    <img src="https://github.com/user-attachments/assets/54e8f607-4f7b-407c-84e2-adce0f33bb04" alt="PowerShell User Creation Screenshot" />
  </p>
</ol>

<h2>Key Takeaways</h2>
<ul>
  <li>Installed and promoted Active Directory Domain Services (AD DS) on a Windows Server 2022 VM, creating a new forest for the domain (`mydomain.com`).</li>
  <li>Created Organizational Units (OUs) and a Domain Admin user, then assigned appropriate security group roles for administrative access.</li>
  <li>Joined a Windows 10 client (Client-1) to the domain and organized it in Active Directory Users and Computers (ADUC).</li>
  <li>Enabled Remote Desktop on Client-1, granting domain users the ability to log in remotely.</li>
  <li>Automated user creation using PowerShell, allowing for bulk user generation to facilitate remote desktop access.</li>
</ul>
