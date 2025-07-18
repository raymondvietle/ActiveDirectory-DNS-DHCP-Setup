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

## Lab Walkthrough

<img width="1023" height="496" alt="image003" src="https://github.com/user-attachments/assets/383c1d95-4988-4976-9278-1c4d76694c01" />

> **Windows Server 2022** was installed on **VMware Workstation Pro** and renamed to `DC01`. A static IP address of `192.168.0.1` was assigned to ensure consistent domain services operation.

<img width="1022" height="728" alt="image004" src="https://github.com/user-attachments/assets/0a904bf3-901c-4026-9368-86cd2d7902c9" />

> From the **Server Manager Dashboard**, I selected "**Add roles and features**" to begin installing essential server roles, including **Active Directory Domain Services (AD DS)**, **DNS**, and **DHCP**. This launched the **Add Roles and Features Wizard**, a step-by-step interface for configuring server functionality.

<img width="856" height="626" alt="image005" src="https://github.com/user-attachments/assets/bfb99c0e-35f1-43b4-85b6-2e256037c799" />

> I launched the **Add Roles and Features Wizard** and confirmed that the required prerequisites were in place—strong administrator password, static IP configuration, and up-to-date patches. After verifying, I proceeded by clicking **Next** to begin the role-based installation process.

<img width="786" height="560" alt="image006" src="https://github.com/user-attachments/assets/7e413eaf-04dd-455f-a992-9e5b105c91c2" />

> I selected "**Role-based or feature-based installation**", which allows configuring this specific server (DC01) by adding individual roles such as **AD DS**, **DNS**, and **DHCP**. This is the most common option for building a traditional on-premises domain controller in a Windows Server environment.

<img width="786" height="560" alt="image007" src="https://github.com/user-attachments/assets/acf598ee-c076-4d8a-a56a-b0102b6542c9" />

> In the **Server Selection** step, I verified that `DC01` (IP: `192.168.0.1`) was listed in the **Server Pool** and selected it to proceed with the role installations.

<img width="787" height="558" alt="image008" src="https://github.com/user-attachments/assets/1f0e915a-584a-4339-8864-64c84f2c935c" />

> I selected **Active Directory Domain Services (AD DS)** to install.  
> This role enables the server to function as a **domain controller**, managing authentication and authorization for users, computers, and resources in the ITRay environment.  
> AD DS allows centralized identity and access management with single sign-on across the domain.

<img width="785" height="556" alt="image009" src="https://github.com/user-attachments/assets/42b8fa09-b4de-4dd0-9dfc-02db5e06dec9" />

> After selecting **Active Directory Domain Services**, I was prompted to install additional management tools required for AD DS.  
> I clicked **"Add Features"** to include tools such as:
> - Group Policy Management
> - AD DS Snap-Ins and Command-Line Tools
> - Active Directory Administrative Center
> - PowerShell modules for AD management  
> These tools are essential for configuring, managing, and troubleshooting Active Directory in a domain environment.

<img width="787" height="559" alt="image010" src="https://github.com/user-attachments/assets/28cb0a36-2843-44b2-a18d-cc9f8c7b7d88" />

> On the **Select Features** screen, I left all options at their defaults.  
> The necessary features for AD DS—such as **Group Policy Management**—were already selected automatically.  
> I clicked **Next** to proceed to the AD DS configuration step.

<img width="785" height="557" alt="image011" src="https://github.com/user-attachments/assets/b195e31c-5b70-4682-b6d7-649a666916ea" />

> The final confirmation screen lists all the roles and features selected for installation, including:
> - Active Directory Domain Services (AD DS)
> - Group Policy Management
> - Remote Server Administration Tools  
> 
> In a **production environment**, it’s recommended to enable automatic restart after role installation.  
> However, since this is a **lab environment**, a restart is not required at this stage.  
> I proceeded by clicking **Install** to begin the installation process.

<img width="784" height="561" alt="image012" src="https://github.com/user-attachments/assets/d483ecff-cf9e-4579-93c4-45a3dacd90c3" />
<img width="1024" height="729" alt="image013" src="https://github.com/user-attachments/assets/e1424cee-f1e4-4024-ac35-98f72ed08a82" />

> Once the role installation completed successfully, a **post-deployment configuration** prompt appeared in Server Manager.  
> I clicked **"Promote this server to a domain controller"** to begin the Active Directory Domain Services configuration and promote `DC01` into a domain controller for the new forest.

<img width="762" height="560" alt="image014" src="https://github.com/user-attachments/assets/20a6bd84-e742-483d-b12f-8091ffeb8fef" />

> I chose **"Add a new forest"** to create a brand new Active Directory environment for the lab.  
> Following best practices for domain naming conventions, I specified the **root domain name** as `int.itray.com`:  
> - `itray.com` simulates a registered external namespace  
> - `int` is prepended to distinguish this as an **internal** domain  
> This approach avoids conflicts with public domains while maintaining proper structure.

<img width="762" height="561" alt="image015" src="https://github.com/user-attachments/assets/79d101c1-f7fa-4489-87ca-0c00e6487eb6" />

> I selected **Windows Server 2016** as the forest and domain functional level for compatibility with modern features.  
> The following default domain controller capabilities were enabled:
> - **Domain Name System (DNS) server**
> - **Global Catalog (GC)**
> 
> I also set a secure **Directory Services Restore Mode (DSRM)** password.  
> This password is used for recovery scenarios and accessing the domain controller in **Directory Services Repair Mode**.

<img width="764" height="562" alt="image016" src="https://github.com/user-attachments/assets/b78bab77-dfd0-4a93-aa4c-68ac8e6ded15" />

> I left **"Create DNS delegation"** unchecked.  
> The warning indicates that a delegation cannot be created because the authoritative parent zone for `itray.com` does not exist—this is expected in a lab environment without a public-facing DNS hierarchy.  
> Since **DNS will be installed locally** on this domain controller (`DC01`), delegation is unnecessary. I clicked **Next** to continue.

<img width="760" height="557" alt="image017" src="https://github.com/user-attachments/assets/45000a19-3e5f-4bff-b689-0c78a41bc66e" />
<img width="761" height="559" alt="image018" src="https://github.com/user-attachments/assets/f28c1890-d8ea-4cbb-aac0-3e21c2f89b47" />

> The setup wizard automatically suggested a **NetBIOS domain name** of `INT`, based on the internal domain `int.itray.com`.  
> However, since the **NetBIOS name is visible to users** when signing in (e.g., `ITRay\username`), I updated it to `ITRay` for a more professional and intuitive experience.

<img width="762" height="561" alt="image019" src="https://github.com/user-attachments/assets/b1d59b02-3cf2-4cea-8aeb-f9ce63b8d03a" />

> All **prerequisite checks passed successfully**, confirming the system is ready to promote the server to a domain controller.  
> While a few warnings were shown (related to DNS delegation and legacy cryptographic settings), these are expected in a lab environment and do not require action.
> 
> I proceeded by clicking **Install**, which triggered the installation of Active Directory Domain Services and automatically restarted the machine upon completion.

<img width="461" height="575" alt="image020" src="https://github.com/user-attachments/assets/2c4cb9e8-4fdd-4ac2-aa76-bca2a0415c42" />

> After the reboot, the login screen now displays the domain name **`ITRay`**, confirming that the domain controller was successfully promoted.  
> Domain users can now sign in using the format:  
> - `ITRay\username` or `username@int.itray.com`  
> This verifies that the NetBIOS name and domain configuration were correctly applied during setup.

<img width="1025" height="633" alt="image021" src="https://github.com/user-attachments/assets/318b59cd-408b-43dd-9f42-98a3bc175089" />

> After promotion and reboot, **Active Directory Domain Services (AD DS)** and **DNS Server** are now listed in the left-hand panel of **Server Manager**.  
> This confirms that the server `DC01` has been successfully configured with both roles, and is now operating as a domain controller with integrated DNS services.

<img width="1025" height="725" alt="image022" src="https://github.com/user-attachments/assets/e7e069c7-ed20-414c-b20f-6f2e6d2d5e08" />

> On the **Local Server** properties page in Server Manager, we can now confirm that the system is joined to the domain **`int.itray.com`**, replacing the default `WORKGROUP` setting.  
> This validates that the domain controller promotion was successful and that the machine is now part of the newly established Active Directory environment.

<img width="1028" height="725" alt="image023" src="https://github.com/user-attachments/assets/4d8b198e-63b7-40e2-9fcf-3b1c54810e74" />

> From **Server Manager**, I navigated to the **Tools** menu and selected **DNS** to open the DNS Manager.  
> This interface allows for configuring forward and reverse lookup zones, managing records, and ensuring name resolution works properly in the newly promoted domain `int.itray.com`.

<img width="1022" height="727" alt="image024" src="https://github.com/user-attachments/assets/63d06ecc-4677-464e-a46c-be7a09f68b0f" />

> Inside **DNS Manager**, under **Forward Lookup Zones → int.itray.com**, we can confirm that the domain controller `DC01` has been automatically registered.  
> The following DNS records are present:
> - **Start of Authority (SOA)** and **Name Server (NS)** records pointing to `dc01.int.itray.com`
> - Two **Host (A)** records for `dc01` resolving to `192.168.0.1`  
> These records validate that the domain controller is discoverable within the network and ready for domain-joined clients to resolve.

<img width="1025" height="725" alt="image025" src="https://github.com/user-attachments/assets/f63c9b3f-4f33-4fc0-8241-2b299348c2f0" />
<img width="1024" height="729" alt="image026" src="https://github.com/user-attachments/assets/1301c6c2-9401-4695-a35e-c8e6243b8b71" />

> I right-clicked the **Start of Authority (SOA)** record under the `int.itray.com` forward lookup zone and selected **Properties**.  
> This opens advanced configuration options for the zone, including:
> - TTL values
> - Primary server settings
> - Serial number and refresh intervals  
> These settings are typically left at defaults in lab environments but can be tuned for performance and replication in production domains.

<img width="1024" height="800" alt="image027" src="https://github.com/user-attachments/assets/30d190f2-0b25-43a4-8fa5-eb5d40d80708" />

> Under the **Name Servers** tab of the `int.itray.com` DNS zone properties, I verified that the name server entry is properly configured.  
> The Fully Qualified Domain Name (FQDN) `dc01.int.itray.com` correctly resolves to the internal IP `192.168.0.1`, confirming that:
> - The domain controller is properly listed as an authoritative name server
> - DNS records are valid and functional for internal resolution  
> This step is key for ensuring reliable DNS queries within the Active Directory environment.

<img width="1019" height="653" alt="image028" src="https://github.com/user-attachments/assets/04e7a76d-566d-458e-a2cf-38cae9780930" />

> Inside the **Edit Name Server Record** window, I verified that the **Fully Qualified Domain Name (FQDN)** `dc01.int.itray.com` is correctly associated with the IP address `192.168.0.1`.  
> The green checkmark and **“Validated: OK”** status confirm that DNS resolution is functional and the entry is fully operational.  
> This ensures reliable name resolution for all domain-joined systems within the network.

<img width="1021" height="724" alt="image029" src="https://github.com/user-attachments/assets/541a17dd-5e08-4138-a4b7-798e56d34d46" />
<img width="1021" height="725" alt="image030" src="https://github.com/user-attachments/assets/6fcb0890-1b8e-4986-a828-bf1f04ea07d7" />

> I noticed that **Reverse Lookup Zones** had not been configured yet in DNS Manager.  
> Reverse zones are important for resolving IP addresses back to hostnames (PTR records), which is often required for diagnostics and authentication.
> 
> To begin, I right-clicked **Reverse Lookup Zones** and selected **New Zone...**, launching the **New Zone Wizard**. I then clicked **Next** to proceed with the setup.

<img width="763" height="531" alt="image031" src="https://github.com/user-attachments/assets/efd2a104-c9f1-4804-8289-920e6f115b9b" />

> I selected **Primary zone**, which allows the zone to be updated directly on this DNS server.  
> This option is ideal for lab environments and standalone domain controllers where DNS is managed locally.
> 
> I left **“Store the zone in Active Directory”** checked, ensuring that the reverse zone is integrated with AD for replication across domain controllers.  
> After confirming the selection, I clicked **Next** to continue.

<img width="1022" height="723" alt="image032" src="https://github.com/user-attachments/assets/932afb9e-3e2c-41c5-811b-508ff40cb2e9" />

> I selected the option to replicate the reverse lookup zone to **“All DNS servers running on domain controllers in this domain: int.itray.com”**.  
> This ensures that if additional domain controllers are introduced within the domain, they will receive a copy of this zone automatically—enhancing **fault tolerance** and **DNS availability** across the environment.

<img width="758" height="532" alt="image033" src="https://github.com/user-attachments/assets/3810b7bc-7130-4283-8b61-571bb5c2730f" />

> I selected **"IPv4 Reverse Lookup Zone"** since my network is based on IPv4 addressing (e.g., `192.168.0.x`).  
> This type of zone allows DNS to resolve IP addresses back into hostnames—essential for tools like `nslookup` and for validating name resolution across the network.

<img width="759" height="533" alt="image034" src="https://github.com/user-attachments/assets/48da6e3b-c32f-44e2-a1c7-6a8b85833768" />

> I set the **Network ID to `192.168.0`**, which defines the range of IP addresses for reverse lookups within this zone.  
> This ensures that as machines (clients, servers, etc.) are added to Active Directory, **reverse DNS records (PTR)** will be automatically created in this zone to support IP-to-hostname resolution.

<img width="755" height="533" alt="image035" src="https://github.com/user-attachments/assets/a51629e6-2142-4894-a708-e95406d1e1d1" />

> Successfully created a **Reverse Lookup Zone**:
>
> - **Name**: `0.168.192.in-addr.arpa`
> - **Type**: Active Directory-Integrated Primary
> - **Lookup Type**: Reverse
>
> This enables **PTR record creation** for reverse DNS resolution. You can now verify name resolution with tools like `nslookup` to ensure dynamic updates occur as machines join the domain.

<img width="757" height="530" alt="image036" src="https://github.com/user-attachments/assets/156ee406-525e-4a63-abc7-1dc06af3014f" />

> From **DNS Manager**, navigate to `Reverse Lookup Zones`.
> Right-click on `0.168.192.in-addr.arpa` and select **Properties**.
> This opens the properties window where you can configure settings for the zone such as **Name Server (NS)** records and **Start of Authority (SOA)**.
> This step is important to ensure proper reverse DNS functionality and designate the authoritative server for this zone.

<img width="1020" height="723" alt="image037" src="https://github.com/user-attachments/assets/df3833c8-ac6b-4d27-b445-221449e48c08" />

> In the **Properties** window of the reverse lookup zone `0.168.192.in-addr.arpa`, under the **Name Servers** tab, you will see the list of configured name servers.
> Select the existing FQDN entry `dc01.int.itray.com.` and click the **Edit...** button.
> This will open the **Edit Name Server Record** window where you can verify or manually input the corresponding IP address of the name server to ensure DNS resolution accuracy.

<img width="1019" height="724" alt="image038" src="https://github.com/user-attachments/assets/91e2773c-660f-4de1-8c66-a3aa321dbe4a" />
<img width="1026" height="726" alt="image039" src="https://github.com/user-attachments/assets/8293768c-ff5d-4f93-a3a0-eb594c172b10" />

> In the **Edit Name Server Record** window, confirm that the FQDN is set to `dc01.int.itray.com.`
> Click the **Resolve** button to automatically fetch and validate the IP address associated with the FQDN.
> If successful, the IP will appear under the "IP Addresses of this NS record" field with a status of **Validated**.

<img width="1022" height="721" alt="image040" src="https://github.com/user-attachments/assets/315e8ce7-b0d0-4758-918b-b59f402dec5a" />

> In the **Forward Lookup Zones**, navigate to `int.itray.com`.
> Locate the **Host (A)** record for `dc01` with IP `192.168.0.1`.
> Right-click on the `dc01` record and select **Properties** to verify details and prepare to create a corresponding **PTR** (reverse lookup) record.

<img width="1021" height="720" alt="image041" src="https://github.com/user-attachments/assets/56a5b5f0-efec-473b-a0fb-911a84d7fa50" />

> In the **Host (A) record Properties** for `dc01`, check the box that says **Update associated pointer (PTR) record**.
> Click **Apply** and then **OK** to save the changes.
> This will automatically generate the PTR record in the **Reverse Lookup Zone**, enabling reverse DNS resolution.

<img width="1016" height="719" alt="image042" src="https://github.com/user-attachments/assets/e53e582e-947f-42bb-ab5a-c2aae3272575" />

> Navigate back to **DNS Manager** and expand the **Reverse Lookup Zones**.
> Select the zone `0.168.192.in-addr.arpa`.
> This allows you to view and confirm the PTR records that were created and are associated with the corresponding IP addresses.

<img width="1016" height="721" alt="image043" src="https://github.com/user-attachments/assets/53ae357c-e3e5-4f52-9938-1a427bce39d9" />

> Click the **Refresh** button in DNS Manager while viewing the `0.168.192.in-addr.arpa` Reverse Lookup Zone.
> Confirm that the **PTR record** for `192.168.0.1` has been successfully created and points to `dc01.int.itray.com.`.
> This confirms reverse DNS resolution is functioning properly for the DC01 host.

#### 📦 Begin DHCP Role Installation

<img width="1018" height="724" alt="image044" src="https://github.com/user-attachments/assets/d4ba0ed9-4485-458c-9a08-c3de51eba90a" />

> Open **Server Manager** and click **Add Roles and Features**.
> The wizard begins with the **Before You Begin** page.
> Click **Next** to proceed with the DHCP Server role installation process.

<img width="1017" height="722" alt="image045" src="https://github.com/user-attachments/assets/0298c15e-012e-441b-9d7d-031e82776967" />

> On the **Select destination server** screen, choose your server (`DC01.int.itray.com`) from the **Server Pool**.
> Confirm the correct IP and OS are listed.
> Click **Next** to continue with the role installation.

<img width="1023" height="723" alt="image046" src="https://github.com/user-attachments/assets/934516c9-24d8-4805-a500-2dfae1c7f961" />

> On the **Select server roles** screen, check the box for **DHCP Server**.
> This role enables your server to assign dynamic IP addresses to client machines.
> Click **Next** to proceed.

<img width="1020" height="723" alt="image047" src="https://github.com/user-attachments/assets/223e2a6e-a2fa-4628-8188-72bea0318c2e" />

> A prompt appears asking to add required features for **DHCP Server**.
> Ensure the **Include management tools (if applicable)** checkbox is selected.
> Click **Add Features** to continue.

<img width="1021" height="721" alt="image048" src="https://github.com/user-attachments/assets/9a3cfbce-793b-40e4-8445-b26ab5ff2bb3" />

> After installing DHCP, return to **Server Manager** and click **Complete DHCP configuration** from the yellow notification flag.
> This step creates the necessary DHCP security groups within Active Directory.
> It's ideal to install DHCP **after** AD DS so that DHCP can recognize and integrate with domain credentials for better management and monitoring.

<img width="1025" height="767" alt="image050" src="https://github.com/user-attachments/assets/94ca0878-3ccb-4163-ac40-6f9ac4c398c9" />

> In the **DHCP Post-Install configuration wizard**, click **Next** to proceed.
> This wizard creates the **DHCP Administrators** and **DHCP Users** security groups and prepares the server for authorization.
> On the **Authorization** screen (not shown), choose **"Use the following user credentials"** and enter the AD DS credentials:
> **Username:** `ITRay\administrator`

<img width="1025" height="766" alt="image052" src="https://github.com/user-attachments/assets/2d525728-2ce8-4abd-8b02-b37ce97bace3" />

> The wizard confirms the successful creation of:
> - **DHCP Administrators** and **DHCP Users** security groups
> - **DHCP Server Authorization** using AD DS credentials

<img width="1027" height="772" alt="image053" src="https://github.com/user-attachments/assets/4873ec7c-bafe-4e23-891d-064822292bd4" />

> Go to **Server Manager** → Click **Tools** → Select **DHCP**.
> 
> This will open the **DHCP Management Console** where we can begin creating a new IPv4 scope.

<img width="1023" height="771" alt="image054" src="https://github.com/user-attachments/assets/5d5d39b2-af10-4fce-9229-8b6c46491088" />
<img width="1023" height="771" alt="image055" src="https://github.com/user-attachments/assets/9f110959-9f4f-4469-b8ed-ed8bf365cc6c" />
<img width="1024" height="771" alt="image056" src="https://github.com/user-attachments/assets/13a1b923-4768-4d4b-ad44-c6cda3bd98bd" />

> In the **DHCP Management Console**, expand your server node (e.g., `dc01.int.itray.com`) → Right-click **IPv4** → Click **New Scope**.
> 
> This will launch the **New Scope Wizard**, which guides you through defining a range of IP addresses for dynamic distribution.

<img width="1025" height="771" alt="image057" src="https://github.com/user-attachments/assets/fbfdb635-b3f0-4b55-8d7f-a23a8961fb51" />

> Entered scope name: **ITRayIPv4**
>
> This name is used to identify the DHCP scope for IPv4 address allocation. A description can optionally be added for clarity.
>
> Click **Next** to proceed.

<img width="1026" height="773" alt="image058" src="https://github.com/user-attachments/assets/f095c339-2647-4388-9c9f-04e8e6dd13e2" />

















































