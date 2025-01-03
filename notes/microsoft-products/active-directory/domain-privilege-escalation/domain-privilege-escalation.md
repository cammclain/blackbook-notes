# Domain Privilege Escalation

---

## Overview

`Domain Privilege Escalation` involves leveraging misconfigurations, excessive permissions, or design flaws within an [Active Directory](../active-directory.md) environment to **gain higher privileges**, typically with the goal of reaching `Domain Admin` or *equivalent access* (e.g. `Enterprise Admin`, or `Enterprise Read-Only Admin`). 

> This process is critical in both red team and penetration testing engagements as it highlights systemic weaknesses that adversaries could exploit.

---

## Techniques for Escalation 🛠️

Below are the major techniques used for domain privilege escalation, each with its own nuances and attack paths. Click on each to dive deeper into specific tactics and methodologies.

1. [Access Control List (ACL) Abuse](./acl-abuse.md)
   - Manipulating permissions to gain elevated access.
   - Exploiting misconfigured [DACLs](../../active-directory/active-directory-access-control-lists.md) and [SACLs](../../active-directory/active-directory-access-control-lists.md).

2. [Delegation Attacks](./delegation-attacks.md)
   - Leveraging unconstrained, constrained, and resource-based delegation to impersonate accounts.

3. [Group Policy Exploitation](./group-policy-exploitation.md)
   - Abusing writable Group Policy Objects (GPOs) to execute code or configure persistence.

4. [Certificate Template Abuse](./certificate-template-abuse.md)
   - Exploiting misconfigured templates in Active Directory Certificate Services (AD CS).

5. [Shadow Credentials](./shadow-credentials.md)
   - Leveraging rogue certificates for stealthy account compromise.

6. [SID History Abuse](sid-history-abuse)
   - Injecting Security Identifiers (SIDs) into accounts for privilege escalation.

---

## Tools for Privilege Escalation 🔧

1. **PowerView**
   ```powershell
   # Enumerate ACLs
   Get-ObjectACL -ResolveGUIDs
   ```

2. **BloodHound**
   - Visualize privilege escalation paths and ACL misconfigurations.

3. **Rubeus**
   ```powershell
   # Perform delegation attacks
   Rubeus.exe tgtdeleg /user:target
   ```

4. **Impacket Suite**
   - Tools like `getST.py` for S4U delegation abuse.

5. **Certify**
   - Discover and exploit misconfigured certificate templates.

---

## OPSEC Considerations 🕵️‍♂️

- Use minimal changes to the target environment to avoid detection.
- Test techniques in isolated lab environments before using them on live engagements.
- Be cautious of noisy operations, such as mass ACL enumeration.

---

## Lab Resources 📚

1. **Practice Scenarios**
   - [TryHackMe AD Labs](https://tryhackme.com)
   - [HackTheBox Pro Labs](https://hackthebox.com)

2. **Simulation Tools**
   - [ADLab](https://github.com/Orange-Cyberdefense/GOAD)
   - [Detection Lab](https://github.com/clong/DetectionLab)

---

## Related Pages 🔗

- [Active Directory](../active-directory.md)
- [Attacking Active Directory](attacking-active-directory)

---

> 💡 **Pro Tip**: Thoroughly document the steps and outcomes of your privilege escalation attempts. This not only helps with reporting but also improves your understanding of the concepts.

---
