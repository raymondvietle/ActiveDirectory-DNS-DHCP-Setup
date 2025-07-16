# 🏢 ITRay Corporation - Simulated Windows Server Infrastructure

## ✨ Overview
I created a fictional organization called **ITRay** to simulate an enterprise-level Windows Server environment. This project demonstrates the configuration and management of core IT services including **Active Directory**, **DNS**, and **DHCP**. The environment models role-based access control for different types of staff.

<img width="100%" height="100%" alt="ITRay Infrastructure" src="https://github.com/user-attachments/assets/28d3708a-96ea-4269-8fb2-0f50e5771bc2" />


---

## 🛠️ Infrastructure Components

**Server**: `DC01` – *Windows Server 2022*
- Roles Installed:
  - **Active Directory Domain Services (AD DS)**
  - **Domain Name System (DNS)**
  - **Dynamic Host Configuration Protocol (DHCP)**
- Static IP Address: `192.168.0.1`

**Client**: `PC01` – *Windows 11*
- DHCP enabled (receives IP from DC01)
- Successfully joined the `int.itray.com` domain
- Domain users can log in based on group membership

---

## 👥 Active Directory Design

**Domain**: `int.itray.com`

**Organizational Unit (OU)**: `ITRay`
- Sub-OUs:
  - `IT`
    - User: `Steve Jobs` *(IT Staff – elevated privileges)*
  - `Staff`
    - User: `Tim Cook` *(Regular Staff – limited permissions)*

**Permissions & GPOs**:
- Applied different Group Policy Objects to control access:
  - IT users have administrative rights and access to IT shares
  - Staff users have standard permissions for regular tasks

---

## 🚪 DHCP Configuration
- Scope: `192.168.0.50` – `192.168.0.200`
- Leases are provided dynamically to client machines

---

## 🧪 Troubleshooting & Tools Used
- **DNS Event ID 4013 Fix**: Resolved startup delay by configuring DNS forwarders and ensuring AD replication
- **DNS Request Timed Out Issue**: Fixed by changing VM network settings to **Host-Only Adapter**
- Used tools:
  - `nslookup`
  - `ping`
  - `ipconfig`

---

## 🎓 Key Skills Demonstrated
- Installing and configuring Windows Server roles
- Managing Active Directory OUs and user accounts
- Setting up DHCP scopes and IP management
- Troubleshooting network and DNS issues in a virtual lab
- Implementing role-based access via GPOs

---

## 📍 Notes
- Project run using **VMware Workstation**
- All firewalls disabled during configuration testing
- Successfully connected both Windows 10 and Windows 11 clients to the domain

