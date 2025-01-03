# Active Directory

---

# Part 1: Understanding `Active Directory`

`Active Directory` is a directory service that *Microsoft* provides for [Windows domain networks](https://search.brave.com/search?q=windows+domain+networks&source=desktop&conversation=8b0d02b21f17136ed5dce5&summary=1). It is used to manage user accounts, computers, and other resources in a network.


## Features of Active Directory

- **Centralized Management**: Active Directory provides a centralized location for managing user accounts, computers, and other resources in a network.
- **Authentication**: Active Directory provides a single sign-on and access platform for enterprise systems.
- **Authorization**: Active Directory provides a flexible directory service for directory-enabled applications.
- **Security**: Active Directory provides information protection technology for sensitive documents.
- **Legacy**: Active Directory provides a legacy lightweight directory service (replaced by AD LDS).

## Active Directory Domain Services

`Active Directory Domain Services` is a component of `Active Directory` that *provides a centralized location for network administration and security*. It is used to manage user accounts, computers, and other resources in a network.

These are some of the technologies that are part of `Active Directory Domain Services`:

- **Active Directory Domain Services**: Central location for network administration and security
- **Active Directory Lightweight Directory Services**: Flexible directory service for directory-enabled applications
- **Active Directory Certificate Services**: Public key infrastructure (PKI) for issuing and managing digital certificates
- **Active Directory Rights Management Services**: Information protection technology for sensitive documents
- **Active Directory Application Mode**: Legacy lightweight directory service (replaced by AD LDS)

## Active Directory Federation Services

`Active Directory Federation Services` is a component of `Active Directory` that provides a single sign-on and access platform for enterprise systems. It is used to manage user accounts, computers, and other resources in a network.

## Active Directory Lightweight Directory Services

`Active Directory Lightweight Directory Services` is a component of `Active Directory` that provides a flexible directory service for directory-enabled applications. It is used to manage user accounts, computers, and other resources in a network.

## Active Directory Certificate Services

`Active Directory Certificate Services` is a component of `Active Directory` that provides a public key infrastructure (PKI) for issuing and managing digital certificates. It is used to manage user accounts, computers, and other resources in a network.

## `Active Directory` Rights Management Services

`Active Directory` *Rights Management Services* is a component of `Active Directory` that *provides information protection technology for sensitive documents*. It is used to manage user accounts, computers, and other resources in a network.

## `Active Directory` Application Mode

`Active Directory` *Application Mode* is a component of `Active Directory` that *provides a legacy lightweight directory service (replaced by AD LDS)*. It is used to manage user accounts, computers, and other resources in a network.


---

# Part 2: Attacking `Active Directory` 🎯

## Overview

`Active Directory` (AD) is the **backbone of modern enterprise networks**, making it a *critical target* for red teamers and penetration testers. Understanding AD's architecture, security mechanisms, and common misconfigurations is essential for successful offensive operations.

## Core Components & Attack Surfaces 🔍

### 1. Domain Controllers (DCs)
- Primary targets in most engagements
- Store the `NTDS.dit` database (contains all domain hashes)
- Host critical services:
  - DNS
  - Kerberos KDC
  - LDAP
  - File Replication

### 2. Authentication Mechanisms
#### Kerberos
- Default authentication protocol
- Common attack vectors:
  - 🎫 Kerberoasting (targeting SPN accounts)
  - 🎭 Pass-the-Ticket (TGT/TGS manipulation)
  - ⚡ Golden/Silver Ticket attacks
  - 🔄 AS-REP Roasting (accounts with "Don't require Kerberos pre-authentication")

#### NTLM
- Legacy authentication protocol
- Attack techniques:
  - 📦 Pass-the-Hash
  - 🔄 NTLM Relay
  - ⚡ SMB Signing abuse

### 3. Critical Objects & Permissions
- **Users & Groups**:
  - Domain Admins
  - Enterprise Admins
  - Schema Admins
  - Backup Operators
  - Account Operators
- **Service Accounts**:
  - Often overlooked
  - Frequently over-privileged
  - Prime targets for credential theft

## Essential Tools for AD Assessment 🛠️

### Enumeration & Reconnaissance
1. **BloodHound**
   - Maps attack paths
   - Identifies privilege escalation routes
   - Visualizes domain relationships
   ```powershell
   # Collection using SharpHound
   ./SharpHound.exe -c all --zipfilename output.zip
   ```

2. **PowerView**
   ```powershell
   # Find domain admins
   Get-NetGroupMember "Domain Admins"
   
   # Enumerate shares
   Find-DomainShare -CheckShareAccess
   ```

3. **ADRecon**
   - Comprehensive AD data collection
   - Excel report generation
   - OPSEC-safe options

### Exploitation Tools
1. **Impacket Suite**
   - secretsdump.py
   - psexec.py
   - GetNPUsers.py
   - GetUserSPNs.py

2. **Rubeus**
   ```powershell
   # Kerberoasting
   Rubeus.exe kerberoast /outfile:hashes.txt
   
   # Pass-the-Ticket
   Rubeus.exe asktgt /user:admin /rc4:[NTLM hash]
   ```

## Advanced Attack Techniques 🚀

### 1. Lateral Movement
- WMI
- PsExec
- DCOM
- PowerShell Remoting
- RDP

### 2. Persistence Mechanisms
- Golden Tickets (domain-wide)
- Silver Tickets (service-specific)
- DCShadow
- AdminSDHolder modifications
- SID History abuse

### 3. Domain Privilege Escalation
- ACL abuse
- Delegation attacks
- Group Policy exploitation
- Certificate template abuse
- Shadow Credentials

## OPSEC Considerations 🕵️

### Detection Evasion
1. **Avoid Noisy Operations**
   - Limit failed authentication attempts
   - Use targeted enumeration
   - Leverage living-off-the-land binaries

2. **Timing & Throttling**
   - Space out operations
   - Match normal business hours
   - Avoid mass enumeration

3. **Tool Selection**
   - Use built-in Windows tools where possible
   - Avoid known malicious indicators
   - Consider custom tooling for critical operations

## Lab Resources 📚

1. **Practice Environments**
   - [TryHackMe Active Directory Labs](https://tryhackme.com)
   - [HackTheBox Pro Labs](https://hackthebox.com)
   - [Detection Lab](https://github.com/clong/DetectionLab)

2. **Build Your Own Lab**
   - Windows Server evaluation VMs
   - Windows 10/11 enterprise evaluation
   - Automated deployment scripts

> 💡 **Pro Tip**: Always maintain detailed documentation of your findings and techniques. AD environments are complex, and good notes are invaluable for both learning and reporting.

---
