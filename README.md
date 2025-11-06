# Active Directory Home Lab Project

## 🎯 Objectives
The objective of this project was to design and deploy a small-scale Active Directory (AD) environment in a virtualized lab setting.  
The lab demonstrates core IT administration and networking competencies, including domain controller deployment, DNS configuration, static IP management, and domain client integration.  
This project simulates a real-world enterprise environment, similar to what Help Desk or Systems Administrators manage daily.

---

## 🧩 Lab Environment

| Component  | Operating System    | Role                                       | IP Address     | Notes                                |
|------------|---------------------|--------------------------------------------|----------------|--------------------------------------|
| DC1       | Windows Server 2025  | Primary Domain Controller (AD DS + DNS)    | 192.168.77.10 | Root of the domain `corp.local`       |
| DC2       | Windows Server 2025  | Secondary Domain Controller (Replication)  | 192.168.77.11 | Ensures fault tolerance               |
| CLIENT01   | Windows 10/11       | Domain-Joined Workstation                  | 192.168.77.20 | Used to simulate end-user environment |

All machines were hosted in **Oracle VirtualBox** using a **Host-Only network** to enable internal communication between virtual machines while isolating the environment from the internet.

---

## 🧠 Key Concepts Demonstrated
- Active Directory Domain Services (AD DS) installation and configuration  
- DNS setup and name resolution troubleshooting  
- Domain controller replication and failover  
- Network configuration using static IPv4 addressing  
- Group Policy management  
- User and organizational unit (OU) administration  
- Domain client joining and authentication testing  

---

## ⚙️ Implementation Steps

### Step 1 – Virtual Network Configuration
- Created a **Host-Only Adapter** in VirtualBox to isolate the lab environment.  
- Assigned the subnet `192.168.77.0/24` for internal routing.  
- Ensured each virtual machine had a **static IPv4 address** and correct DNS configuration (pointing to DC1).
### VirtualBox Network Setup  
![VirtualBox Host-Only Network Overview](Screenshots/virtualbox_vms_overview.png)

### DC01 Network Settings  
![DC01 Static IP Configuration](Screenshots/dc01_network_settings.png)

### DC02 Network Settings  
![DC02 Static IP Configuration](Screenshots/dc02_network_settings.png)

### Step 2 – Primary Domain Controller (DC1)
- Installed **Windows Server 2025** and configured a static IP: `192.168.77.10`.  
- Renamed the host to `DC1`.  
- Installed **Active Directory Domain Services (AD DS)** and promoted the server as the first domain controller for `corp.local`.  
- Verified successful DNS resolution using:
  ```powershell
  nslookup dc1.corp.local
  ```
- Confirmed functionality by testing logon and administrative tools (ADUC, DNS Manager).
- ### Active Directory Installation Wizard  
![Installing AD DS on DC01](Screenshots/dc01_ad_install.png)

### AD DS Installation Succeeded  
![AD DS Installation Success Confirmation](Screenshots/dc01_ad_install_succeed.png)

### DNS Zone Created for corp.local  
![corp.local DNS Zone Configuration](Screenshots/dc01_dns_zone.png)


### Step 3 – Secondary Domain Controller (DC2)
- Installed **Windows Server 2025**, static IP: `192.168.77.11`, DNS pointed to `192.168.77.10`.  
- Joined `corp.local` domain as a member server.  
- Promoted to **Domain Controller** to establish AD replication and redundancy.  
- Validated replication using:
  ```powershell
  repadmin /replsummary
  ```
- Confirmed both DCs responded to DNS and authentication requests.
- ### DC2 Promoted to Domain Controller  
![DC02 Domain Controller Promotion Success](Screenshots/dc2_promotion_success_.png)

### Replication Verification  
![Replication Summary After Join](Screenshots/dc2_replsummary_after_join.png)


### Step 4 – Domain Client (CLIENT01)
- Installed **Windows 10/11**, static IP: `192.168.77.20`, DNS: `192.168.77.10`.  
- Joined the `corp.local` domain successfully.  
- Verified domain connectivity using:
  ```powershell
  whoami
  ```
- Logged in using a domain user account created via **Active Directory Users and Computers**.
- ### Client Network Configuration  
![CLIENT01 Static IP and DNS Settings](Screenshots/client01_network_config.png)

### Connectivity Test  
![CLIENT01 Ping and Nslookup Results](Screenshots/client01_ping_nslookup.png)

### Domain Join Success  
![CLIENT01 Successfully Joined corp.local](Screenshots/client01_domain_join_success.png)

### Verify Domain Membership  
![CLIENT01 Domain Membership Confirmation](Screenshots/client01_verify_domain_membership.png)

### Login Test with Domain Account  
![Login with Domain Admin](Screenshots/client01_login_domain_admin.png)


### Step 5 – Group Policy & User Management
- Created Organizational Units (OUs) for `Users`, `Computers`, and `Admins`.  
- Configured a sample Group Policy Object (GPO) to enforce password complexity.  
- Tested GPO application using:
  ```powershell
  gpupdate /force
  gpresult /r
  ```
### Created Organizational Units  
![OUs for Users, Computers, and Admins](Screenshots/dc1_created_organizational_units.png)

### Password Complexity Policy Configured  
![Password Complexity GPO Configuration](Screenshots/dc1_gpo_password_complexity.png)

### GPO Applied Successfully  
![GPO Result Shown on Client01](Screenshots/client01_gpresult_gpo_applied.png)

### Password Policy Verified  
![Password Complexity Policy Verified](Screenshots/client01_Password_Complexity_Policy_Applied.png)

## 📁 File Sharing Test
### Shared Folder Configuration on DC1  
![DC1 Shared Folder Properties](Screenshots/dc1_share_folder_properties.png)

### Accessing the Share from Client01  
![Accessing Shared Folder from Client01](Screenshots/client01_access_share_explorer.png)



---

## 🧾 Disclosure and Assumptions
- This lab was conducted purely for **educational and training purposes**.  
- All systems were deployed in a **virtualized, isolated environment** using Oracle VirtualBox.  
- No production networks or external systems were impacted.  
- IP addresses and domain names used are **non-routable and fictional** (`corp.local`).  
- Windows Server 2025 was used to simulate modern enterprise infrastructure but follows the same procedures as Windows Server 2019/2022.  

---

## 🧩 What I Learned
Through this project, I developed hands-on experience with core IT infrastructure principles, including:

- Configuring **Active Directory and DNS** from the ground up.  
- Managing **user accounts, OUs, and group policies**.  
- Implementing **domain controller redundancy** through replication.  
- Troubleshooting **DNS, name resolution, and network connectivity** issues.  
- Understanding **how clients authenticate to a domain** and interact with directory services.  
- Building confidence in **Windows Server administration**, virtualization, and network design.

This project solidified my understanding of how enterprise networks operate internally and provided a strong foundation for entry-level IT support, Help Desk, and system administration roles.

---

## 📚 Tools and Technologies Used
- Oracle VirtualBox  
- Windows Server 2025  
- Windows 10/11 Enterprise  
- Active Directory Domain Services (AD DS)  
- DNS Manager  
- Group Policy Management Console (GPMC)  
- PowerShell  

---

## 🏁 Conclusion
This lab successfully demonstrates a functioning multi-domain controller Active Directory environment within a virtualized network.  
It showcases my ability to design, deploy, and manage Windows-based infrastructures — skills that are directly applicable to IT Help Desk, System Administration, and Cybersecurity operations roles.

---

*Created by Szilard — 2025*
