# DC-01 Overview

## Purpose

`DC-01` is the Windows Server 2022 domain controller for the PrimeSec Infrastructure environment.

It hosts the `primesec.local` Active Directory domain and provides Active Directory Domain Services, Active Directory Integrated DNS, and Group Policy management.

---

## Environment Role

`DC-01` is the identity and internal DNS authority for the Windows domain.

Domain-joined systems use `DC-01` for authentication, Active Directory service discovery, internal domain name resolution, and Group Policy processing.

---

## System Summary

| Property | Value |
| -------- | -------- |
| Component | `DC-01` |
| Operating System | Windows Server 2022 |
| Virtualization Platform | Proxmox VE |
| Role | Domain controller |

---

## Network Summary

| Property | Value |
| -------- | -------- |
| Network | `10.10.10.0/24` |
| IP Address | `10.10.10.10` |
| Default Gateway | `FW-01` / `10.10.10.1` |
| Domain | `primesec.local` |

The Active Directory NetBIOS name is `PRIMESEC`. DNS for the domain is provided through Active Directory Integrated DNS on `DC-01`.

---

## Key Functions

### Active Directory Domain Services

`DC-01` provides the core directory services for the domain, including:

- Domain authentication
- User and group administration
- Computer account management
- Organizational Unit management
- Centralized Windows administration

The documented Organizational Unit structure separates administrative accounts, groups, servers, users, and workstations.

    PRIMESEC
    ├── Admin
    ├── Groups
    ├── Servers
    ├── Users
    └── Workstations

### DNS

`DC-01` provides Active Directory Integrated DNS for `primesec.local`.

Its DNS responsibilities include:

- Internal name resolution for the AD domain
- Domain controller service discovery
- Active Directory service location
- Forward lookup zone management

`FW-01` remains the default gateway and DHCP provider. `DC-01` remains authoritative for Active Directory DNS.

### Group Policy

`DC-01` manages Group Policy for the domain and workstation configuration.

Implemented policies include:

- `GPO-Domain-Password-Policy`
- `GPO-Interactive-Logon-Notice`
- `GPO-Workstation-Security-Baseline`
- `GPO-Workstation-Windows-Update`

Exported Group Policy reports are stored under `reports/gpo/`.

---

## Related Documentation

| Document | Purpose |
| -------- | -------- |
| [Group Policy](group-policy.md) | Implemented GPOs and exported reports |
| [DNS Configuration](../networking/dns.md) | Internal DNS responsibility model |
| [DC-01 Validation](validation.md) | Validation evidence for AD DS, DNS, and Group Policy |

---

## Validation Reference

`DC-01` validation is documented in [DC-01 Validation](validation.md).

Validation covers:

- Active Directory domain configuration
- Organizational Unit structure
- Active Directory Integrated DNS
- Domain controller health
- Group Policy deployment
- Workstation policy processing on `WS-01`