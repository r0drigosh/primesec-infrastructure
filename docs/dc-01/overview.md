# DC-01 Overview

## Purpose

`DC-01` is the Windows Server 2022 domain controller for the PrimeSec Infrastructure environment.

It hosts the `primesec.local` Active Directory domain and provides Active Directory Domain Services, Active Directory Integrated DNS, and Group Policy management.

---

## Environment Role

`DC-01` is the central identity, authentication, internal DNS, and Group Policy management component for the Windows domain.

Domain-joined systems use `DC-01` for:

- Domain authentication
- Active Directory service discovery
- Internal `primesec.local` name resolution
- Group Policy processing

`FW-01` remains the internal gateway and DHCP provider. `FW-01` distributes `DC-01` / `10.10.10.10` as the DNS server for domain clients.

---

## System Summary

| Property | Value |
| --- | --- |
| Component | `DC-01` |
| Operating system | Windows Server 2022 |
| Virtualization platform | Proxmox VE |
| Role | Domain controller, AD DS, DNS, Group Policy |
| Domain | `primesec.local` |
| NetBIOS name | `PRIMESEC` |

---

## Network Summary

| Property | Value |
| --- | --- |
| Internal network | `10.10.10.0/24` |
| IP address | `10.10.10.10` |
| Default gateway | `FW-01` / `10.10.10.1` |
| AD DNS namespace | `primesec.local` |
| DHCP provider | `FW-01` |

`DC-01` is authoritative for the `primesec.local` Active Directory DNS namespace.

---

## Key Functions

### Active Directory Domain Services

`DC-01` provides the core directory services for the domain.

Its Active Directory role includes:

- Domain authentication
- User and group administration
- Computer account management
- Organizational Unit management
- Centralized Windows administration

The documented OU model separates administrative accounts, groups, servers, users, and workstations.

```text
primesec.local
└── PRIMESEC
    ├── Admin
    ├── Groups
    ├── Servers
    ├── Users
    └── Workstations
```

### DNS

`DC-01` provides Active Directory Integrated DNS for `primesec.local`.

Its DNS role supports:

- Internal domain name resolution
- Domain controller location
- Active Directory service discovery
- Forward lookup zone management
- Domain-joined client operation

`FW-01` provides DHCP and gateway services. `DC-01` remains the authoritative DNS server for the Active Directory namespace.

### Group Policy

`DC-01` manages Group Policy for domain and workstation configuration.

Implemented GPOs include:

- `GPO-Domain-Password-Policy`
- `GPO-Interactive-Logon-Notice`
- `GPO-Workstation-Security-Baseline`
- `GPO-Workstation-Windows-Update`

Exported Group Policy reports are stored under `reports/gpo/`.

---

## Related Documentation

| Document | Purpose |
| --- | --- |
| [Group Policy](group-policy.md) | Implemented GPOs and policy scope |
| [DC-01 Validation](validation.md) | Validation evidence for AD DS, DNS, and Group Policy |
| [DNS Configuration](../networking/dns.md) | DNS and DHCP responsibility model |
| [Group Policy Reports](../../reports/gpo/) | Exported GPO reports |

---

## Validation Reference

`DC-01` validation is documented in [DC-01 Validation](validation.md).

Validation covers:

- Active Directory domain configuration
- Organizational Unit structure
- Active Directory Integrated DNS
- Domain controller health
- Group Policy linking
- Implemented GPO settings