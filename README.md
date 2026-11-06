# VortexDynamics --- Active Directory Lab

A hands-on enterprise IT infrastructure lab built with **VMware
Workstation**, **Windows Server 2022**, and **Windows 11 Pro**.

The project demonstrates virtual machine provisioning, Active Directory
Domain Services (AD DS), DNS, domain joining, centralized user and
computer management, and Group Policy configuration.

## Architecture

``` mermaid
flowchart TB
    subgraph VMware["VMware Workstation — NAT / VMnet8"]
        DC["VD-DC01<br/>Windows Server 2022<br/>192.168.176.10"]
        CLIENT["VD-CLIENT01<br/>Windows 11 Pro<br/>192.168.176.20"]
        DC --- CLIENT
    end

    DC --> AD["Active Directory Domain Services<br/>vortexdynamics.test"]
    DC --> DNS["DNS Server<br/>Forwarder: 8.8.8.8"]
    AD --> OU["Organizational Units<br/>Users · Computers · Groups"]
    AD --> GPO["Group Policy"]
```

## Lab Configuration

  Component              Configuration
  ---------------------- -----------------------------------
  Virtualization         VMware Workstation Pro 17
  Domain controller      `VD-DC01` --- Windows Server 2022
  Client                 `VD-CLIENT01` --- Windows 11 Pro
  Domain                 `vortexdynamics.test`
  NetBIOS name           `VORTEXDYNAMICS`
  Network                NAT / VMnet8
  Domain controller IP   `192.168.176.10`
  Client IP              `192.168.176.20`
  Default gateway        `192.168.176.2`
  DNS                    `192.168.176.10`

## Implementation

### Phase 1 --- Infrastructure Setup

-   Created the `VD-DC01` and `VD-CLIENT01` virtual machines.
-   Configured virtual processors, memory, firmware, storage, and
    network adapters.

[Phase 1
documentation](Phase-01-Infrastructure-Setup/Documentation/Phase-01-Infrastructure-Setup.md)

### Phase 2 --- Active Directory Configuration

-   Installed and configured Windows Server 2022.
-   Installed AD DS and DNS, and promoted `VD-DC01` to a domain
    controller.
-   Configured DNS forwarding and verified name resolution.
-   Configured the Windows 11 client and joined it to the domain.
-   Created departmental OUs, user accounts, and Global Security groups.
-   Added users to their departmental groups and placed the client
    computer account in the IT Computers OU.

[Server installation, AD DS and
DNS](Phase-02-Active-Directory/Documentation/Phase-02-Server-Installation-ADDS-and-DNS.md)\
[Client configuration and AD
objects](Phase-02-Active-Directory/Documentation/Phase-02-Client-Configuration-and-AD-Objects.md)

### Phase 3 --- Group Policy Management

-   Configured domain password policy settings.
-   Created and linked `GPO-USB-Restriction` to the IT Computers OU.
-   Configured removable-disk read, write, and execute restrictions.
-   Created and linked the Control Panel restriction GPO to the
    VortexDynamics Users OU.
-   Refreshed and verified Group Policy on the client.

[Phase 3
documentation](Phase-03-Group-Policy/Documentation/Phase-03-Group-Policy-Management.md)

## Repository Structure

``` text
VortexDynamics-AD-Lab/
├── ISO/
├── Virtual-Machines/
├── Phase-01-Infrastructure-Setup/
│   ├── Documentation/
│   └── Screenshots/
├── Phase-02-Active-Directory/
│   ├── Documentation/
│   └── Screenshots/
├── Phase-03-Group-Policy/
│   ├── Documentation/
│   └── Screenshots/
├── .gitignore
└── README.md
```

Each phase's Markdown guide includes step-by-step instructions with
screenshots stored in the corresponding `Screenshots` folder.

## Tools and Technologies

-   VMware Workstation Pro 17
-   Windows Server 2022
-   Windows 11 Pro
-   Active Directory Domain Services
-   DNS Server
-   Group Policy Management
-   PowerShell and Windows command-line tools

------------------------------------------------------------------------

**Project type:** Hands-on Windows infrastructure and system
administration lab.
