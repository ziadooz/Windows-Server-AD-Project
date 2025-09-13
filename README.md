# Windows Server Active Directory Infrastructure Project 🖥️

**Objective 🎯**
The goal of this project was to build a complete, functional, and redundant IT infrastructure for a sample corporate network from the ground up. This project demonstrates the core skills required for a Systems Administrator role, including server setup, network services configuration, security policy implementation, and storage management in a Windows Server environment.

---

## Network Topology 🌐

The virtual network was built on a 192.168.5.0/24 subnet and consists of several virtual machines configured in Hyper-V to simulate a standard corporate site:

* **HQ-DC-01**: The primary Domain Controller for the CorpNet.local domain. Also hosts DNS and DHCP services.
* **HQ-DC-02**: A secondary Domain Controller providing redundancy for Active Directory, DNS, and DHCP (via failover). Also serves as an iSCSI storage target.
* **HQ-WEB-01**: A web server (IIS) participating in a Network Load Balancing (NLB) cluster.
* **HQ-WEB-02**: A second web server (IIS) providing high availability for the web application through the NLB cluster.
* **HQ-CL-01**: A Windows 10 client machine used for testing and simulating user activity.
* **HQ-CORE-01**: A Windows Server Core machine deployed for future use, demonstrating remote management capabilities.

---

## Key Configurations 🔧

This project involved the end-to-end setup and configuration of a new Active Directory forest. The key tasks completed include:

### Active Directory & DNS 📂

* Established a new Active Directory forest named **CorpNet.local**.
* Deployed and configured two Domain Controllers (**HQ-DC-01, HQ-DC-02**) for high availability.
* Configured DNS forwarders to enable internet name resolution.
* Transferred the Schema Master FSMO role to the secondary DC.

💡  screenshot

---

### Network Services (DHCP & NLB) 📡

* Installed and configured DHCP scopes to provide dynamic IP addressing to clients.
* Established a DHCP Failover relationship (Hot Standby) between the two DCs for redundancy.
* Implemented a Network Load Balancing (NLB) cluster for the web servers to provide a single, highly available web service at **[http://www.corpnet.local](http://www.corpnet.local)**.

💡  screenshot

---

### Group Policy Management 🛡️

* Created a structured **Organizational Unit (OU)** layout for IT, Developers, Servers, and Clients.
* Implemented a **domain-wide interactive logon message**.
* Configured a **Fine-Grained Password Policy** to enforce stricter password rules for a specific administrative user.
* Used **Loopback Processing (Merge Mode)** on the Servers and DCs OUs to control user policy application.
* Applied a **GPO** to restrict access to registry tools for Developers OU, with exceptions.
* Deployed a **policy to block USB drives** and other removable devices.
* Configured **Folder Redirection** for Developers’ *Documents*.
* Used **Group Policy Preferences** to automatically map a network drive.

💡 screenshot

---

### Storage Management 💾

* Installed and configured **FSRM** to block `.exe` and `.ps1` files in a share.
* Built a **RAID 5** software array on **HQ-DC-02** using three virtual disks.
* Configured an **iSCSI Target** on **HQ-DC-02**, provisioning virtual disks from the RAID 5 array for the web servers.

💡  screenshot

---

### Server Deployment ⚙️

* Deployed and configured a **Windows Server Core** installation and successfully joined it to the **CorpNet.local** domain.

---

## Technologies Used 💡

* **Hypervisor**: Microsoft Hyper-V
* **Server OS**: Windows Server 2025
* **Client OS**: Windows 10

**Core Technologies:**

* Active Directory Domain Services (AD DS)
* Domain Name System (DNS)
* Dynamic Host Configuration Protocol (DHCP)
* Group Policy Management
* Network Load Balancing (NLB)
* File Server Resource Manager (FSRM)
* iSCSI Target and Initiator

**Management Tools:**

* Server Manager, ADUC, Group Policy Management Console, DNS Manager, DHCP Manager, FSRM, Disk Management
* PowerShell ⚡ (for FSMO role verification)
