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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>

</p>
<p>
**Setup Resources in Azure**

**Step 1: Create Domain Controller VM (Windows Server 2022)**
- Create a Windows Server 2022 VM named “DC-1” in Azure.
- Take note of the Resource Group and Virtual Network (Vnet) created during this process.
- Set Domain Controller’s NIC Private IP address to be static.

**Step 2: Create Client VM (Windows 10)**
- Create a Windows 10 VM named “Client-1” in the same Resource Group and Vnet from Step 1.
- Ensure both VMs are in the same Vnet (verify using Network Watcher).

**Step 3: Ensure Connectivity between Client and Domain Controller**
- Login to Client-1 using Remote Desktop and perpetually ping DC-1’s private IP address.
- On DC-1, enable ICMPv4 on the local Windows Firewall.
- Verify successful ping from Client-1.

**Step 4: Install Active Directory**
- Login to DC-1 and install Active Directory Domain Services.
- Promote DC-1 as a DC, setting up a new forest (e.g., mydomain.com).
- Restart and log back into DC-1 as user: mydomain.com\labuser.

**Step 5: Create Admin and Normal User Account in AD**
- In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) named “_EMPLOYEES.”
- Create an OU named “_ADMINS.”
- Create a new employee named “Jane Doe” with the username “jane_admin.”
- Add jane_admin to the “Domain Admins” Security Group.
- Log in as “mydomain.com\jane_admin.”

**Step 6: Join Client-1 to Your Domain (mydomain.com)**
- Set Client-1’s DNS settings in Azure Portal to DC’s Private IP address.
- Restart Client-1 from Azure Portal.
- Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart).
- Verify Client-1 shows up in ADUC inside the “Computers” container on the root of the domain.
- Optionally, create an OU named “_CLIENTS” and move Client-1 into it.

**Step 7: Setup Remote Desktop for Non-administrative Users on Client-1**
- Log into Client-1 as mydomain.com\jane_admin and open system properties.
- Click “Remote Desktop” and allow “domain users” access to remote desktop.
- Log into Client-1 as a normal, non-administrative user.

**Step 8: Create Additional Users and Attempt to Log into Client-1**
- Login to DC-1 as jane_admin.
- Open PowerShell_ise as an administrator.
- Create a new File and paste the contents of the script from [here](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1).
- Run the script and observe the accounts being created.
- Check ADUC to verify the accounts in the appropriate OU.
- Attempt to log into Client-1 with one of the newly created accounts (note the password from the script).
</p>
<br />


