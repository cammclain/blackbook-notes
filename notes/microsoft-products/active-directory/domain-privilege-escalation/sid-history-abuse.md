---
id: sid-history-abuse
title: SID History Abuse
desc: 'Understanding and Mitigating SID History Abuse in Windows Environments'
updated: 1735911717252
created: 1735911158539
---

# SID History Abuse

SID History Abuse is a technique used to impersonate users in Windows environments by manipulating Security Identifier (SID) history attributes. This attack vector can lead to unauthorized privilege escalation and access to restricted resources.

## Overview

### What is a SID?
A Security Identifier (SID) is a unique identifier used in Windows systems to identify users, groups, and other security principals. Each SID is guaranteed to be unique within its domain.

### Understanding SID History
SID History is a feature designed to maintain access to resources when user accounts are migrated between domains. It stores previous SIDs associated with an account, allowing seamless access to resources in both the old and new domains.

## Attack Methods

### Pre-Windows 2016
- **Tool**: Mimikatz
- **Command**: `sid::patch`
- **Limitation**: Only works on domain controllers before Windows Server 2016

### Windows 2016 and Later
- **Tool**: DSInternals PowerShell Module
- **Process**:
  1. Stop NTDS service
  2. Inject the SID
  3. Restart the service

## Impact

When successfully exploited, SID History Abuse can lead to:
- Privilege escalation
- Unauthorized access to protected resources
- Security control bypass
- Domain-wide compromise

## Prevention and Detection

### Security Controls
1. Implement strong password policies
2. Monitor SID History modifications
3. Limit account privileges
4. Regular security audits

### Best Practices
- Regularly review SID History attributes
- Implement least-privilege access
- Use modern authentication mechanisms
- Monitor domain controller logs

## Attack Flow Diagram

```mermaid
graph TD
    A[SID History Abuse] --> B[Security Identifier (SID)]
    B --> C["Unique ID for users or groups in AD"]
    A --> D[SID History]
    D --> E["List of previous SIDs for an account"]
    A --> F[Abuse Process]
    F --> G[Modify SID History]
    G --> H["Add forged SIDs to token's SID history"]
    H --> I["Impersonate user or group linked to added SID"]

    A --> J[Impact of Abuse]
    J --> K["Privilege Escalation"]
    J --> L["Access Resources Without Authorization"]
    J --> M["Bypass Security Controls"]

    A --> N[Exploitation Tools]
    N --> O[Mimikatz]
    O --> P["Add SIDs on pre-Windows 2016 DCs"]
    N --> Q[DSInternals PowerShell]
    Q --> R["Add SIDs on Windows 2016+ DCs"]

    A --> S[Defensive Measures]
    S --> T["Monitor SID History Changes"]
    S --> U["Limit Account Privileges"]
    S --> V["Use Strong Authentication Mechanisms"]

    style A fill:#000,stroke:#fff,color:#fff
    style B fill:#fff,stroke:#000,color:#000
    style D fill:#fff,stroke:#000,color:#000
    style F fill:#fff,stroke:#000,color:#000
    style J fill:#fff,stroke:#000,color:#000
    style N fill:#fff,stroke:#000,color:#000
    style S fill:#fff,stroke:#000,color:#000
```

## References
- [Microsoft Documentation on SID History](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-identifiers)
- [MITRE ATT&CK - SID History Abuse](https://attack.mitre.org/techniques/T1134/005/)
