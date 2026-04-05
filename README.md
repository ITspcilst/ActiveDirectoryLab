# 🏢 Active Directory Home Lab Project

> A multi-domain controller Active Directory lab built in a virtualized environment to simulate real-world enterprise infrastructure, including DNS, replication, Group Policy, and domain client management.

---

## 📌 Overview

This project demonstrates the deployment and configuration of a **Windows Active Directory environment** using multiple domain controllers and a domain-joined client.

The lab simulates a **small enterprise network**, where core services such as authentication, DNS resolution, Group Policy, and file sharing are centrally managed.

The environment was built using **Oracle VirtualBox** with an isolated network, allowing safe testing of enterprise-level configurations without affecting external systems.

---

## 🎯 Objectives

- Deploy and configure **Active Directory Domain Services (AD DS)**
- Implement **DNS infrastructure** for domain resolution
- Configure **multi-domain controller replication**
- Manage **users, OUs, and Group Policies**
- Join and validate a **domain client machine**
- Simulate real-world **IT administration workflows**

---

## 🧩 Lab Environment

| Component  | Operating System    | Role                                       | IP Address     | Notes                                |
|------------|---------------------|--------------------------------------------|----------------|--------------------------------------|
| DC1        | Windows Server 2025 | Primary Domain Controller (AD DS + DNS)    | 192.168.77.10 | Root domain: `corp.local`             |
| DC2        | Windows Server 2025 | Secondary Domain Controller (Replication)  | 192.168.77.11 | Redundancy and failover              |
| CLIENT01   | Windows 10/11       | Domain-Joined Workstation                  | 192.168.77.20 | End-user simulation                  |

---

## 🌐 Network Configuration

- Virtualization platform: **Oracle VirtualBox**
- Network type: **Host-Only Adapter**
- Subnet: `192.168.77.0/24`
- Internal DNS: Pointed to **DC1**

### VirtualBox Network Setup  
![VirtualBox Host-Only Network Overview](Screenshots/virtualbox_vms_overview.png)

### DC01 Network Settings  
![DC01 Static IP Configuration](Screenshots/dc01_network_settings.png)

### DC02 Network Settings  
![DC02 Static IP Configuration](Screenshots/dc02_network_settings.png)

---

## 🧠 Key Concepts Demonstrated

- Active Directory Domain Services (**AD DS**) deployment  
- DNS configuration and name resolution  
- Domain controller replication and redundancy  
- Static IP configuration in enterprise environments  
- Group Policy creation and enforcement  
- User and Organizational Unit (OU) management  
- Domain join and authentication processes  

---

## ⚙️ Implementation

### 🔹 Step 1 – Network Setup

- Configured isolated Host-Only network
- Assigned static IP addresses to all machines
- Configured DNS to point to DC1

---

### 🔹 Step 2 – Primary Domain Controller (DC1)

- Installed Windows Server 2025  
- Configured static IP (`192.168.77.10`)  
- Installed AD DS role  
- Promoted server to domain controller for `corp.local`  
- Verified DNS functionality  

```powershell
nslookup dc1.corp.local
```

### AD DS Installation  
![Installing AD DS on DC01](Screenshots/dc01_ad_install.png)

### Installation Success  
![AD DS Installation Success Confirmation](Screenshots/dc01_ad_install_succeed.png)

### DNS Zone Configuration  
![corp.local DNS Zone Configuration](Screenshots/dc01_dns_zone.png)

---

### 🔹 Step 3 – Secondary Domain Controller (DC2)

- Installed Windows Server 2025  
- Joined domain as member server  
- Promoted to Domain Controller  
- Enabled replication and redundancy  

```powershell
repadmin /replsummary
```

### DC2 Promotion  
![DC02 Domain Controller Promotion Success](Screenshots/dc2_promotion_success_.png)

### Replication Check  
![Replication Summary After Join](Screenshots/dc2_replsummary_after_join.png)

---

### 🔹 Step 4 – Domain Client (CLIENT01)

- Installed Windows 10/11  
- Configured static IP and DNS  
- Joined `corp.local` domain  
- Tested authentication and connectivity  

```powershell
whoami
```

### Client Network Config  
![CLIENT01 Static IP and DNS Settings](Screenshots/client01_network_config.png)

### Connectivity Test  
![CLIENT01 Ping and Nslookup Results](Screenshots/client01_ping_nslookup.png)

### Domain Join  
![CLIENT01 Successfully Joined corp.local](Screenshots/client01_domain_join_success.png)

### Membership Verification  
![CLIENT01 Domain Membership Confirmation](Screenshots/client01_verify_domain_membership.png)

### Login Test  
![Login with Domain Admin](Screenshots/client01_login_domain_admin.png)

---

### 🔹 Step 5 – Group Policy & User Management

- Created Organizational Units (OUs)  
- Implemented password complexity policy  
- Tested GPO application  

```powershell
gpupdate /force
gpresult /r
```

### OU Structure  
![OUs for Users, Computers, and Admins](Screenshots/dc1_created_organizational_units.png)

### GPO Configuration  
![Password Complexity GPO Configuration](Screenshots/dc1_gpo_password_complexity.png)

### GPO Result  
![GPO Result Shown on Client01](Screenshots/client01_gpresult_gpo_applied.png)

### Password Policy Applied  
![Password Complexity Policy Verified](Screenshots/client01_Password_Complexity_Policy_Applied.png)

---

## 📁 File Sharing Test

### Shared Folder Setup  
![DC1 Shared Folder Properties](Screenshots/dc1_share_folder_properties.png)

### Access from Client  
![Accessing Shared Folder from Client01](Screenshots/client01_access_share_explorer.png)

---

## 🧠 Key Learning Outcomes

- Built and managed a full **Active Directory environment**
- Configured **DNS and domain-based authentication**
- Implemented **redundancy using multiple domain controllers**
- Applied **Group Policies in a controlled environment**
- Troubleshot network and domain connectivity issues
- Gained hands-on experience with **Windows Server administration**

---

## 🔒 Real-World Relevance

This project reflects responsibilities typically performed by:

- IT Support / Help Desk Engineers  
- Junior System Administrators  
- Infrastructure Support Technicians  

Key real-world applications include:

- User account management  
- Password policy enforcement  
- Domain authentication troubleshooting  
- Network and DNS issue resolution  
- Access control and file sharing  

---

## ⚠️ Limitations & Future Improvements

### Current Limitations
- No DHCP implementation  
- No advanced Group Policy configurations  
- No monitoring tools (e.g., Event Logs analysis)

### Planned Improvements
- Implement DHCP server  
- Add advanced GPOs (USB restrictions, login scripts)  
- Configure file permissions using security groups  
- Integrate monitoring and logging  
- Simulate real help desk tickets  

---

## 🎤 How to Explain This in an Interview

> I built a multi-domain controller Active Directory lab using Windows Server in a virtualized environment. I configured DNS, set up domain replication, created users and Group Policies, and joined a client machine to the domain. This helped me understand how enterprise authentication and infrastructure work, and gave me hands-on experience troubleshooting real-world IT scenarios.

---

## 🏁 Conclusion

This project demonstrates the ability to design, deploy, and manage a Windows-based Active Directory infrastructure.

It reflects practical, job-relevant skills required for **Help Desk, IT Support, and Junior System Administration roles**.

---

*Created by Szilard — 2025*