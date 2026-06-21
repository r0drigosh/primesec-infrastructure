# WS-01 Overview

## Purpose

`WS-01` is the managed Windows workstation in the PrimeSec Infrastructure environment.

It runs Windows 11 Pro, is joined to the `primesec.local` domain, receives network configuration through DHCP, and processes workstation configuration through Active Directory Group Policy.

---

## Environment Role

`WS-01` represents a standard internal Windows client on the infrastructure network.

It is used to validate workstation integration with the domain, including DHCP addressing, Active Directory DNS dependency, computer Group Policy processing, and the interactive logon notice.

---

## System Summary

| Property | Value |
| --- | --- |
| Component | `WS-01` |
| Operating system | Windows 11 Pro |
| Virtualization platform | Proxmox VE |
| Role | Domain-joined Windows workstation |
| Domain | `primesec.local` |

---

## Network and Domain Summary

| Property | Value |
| --- | --- |
| Internal network | `10.10.10.0/24` |
| DHCP provider | `FW-01` |
| DHCP scope | `10.10.10.100 - 10.10.10.199` |
| Observed DHCP lease | `10.10.10.152` |
| Lease type | `dynamic` |
| Default gateway | `FW-01` / `10.10.10.1` |
| DNS server | `DC-01` / `10.10.10.10` |
| DNS namespace | `primesec.local` |

`WS-01` receives its address dynamically from the `FW-01` DHCP scope.

`FW-01` provides DHCP and gateway services. `DC-01` remains authoritative for the `primesec.local` Active Directory DNS namespace.

---

## Key Functions

### Domain Client

`WS-01` is joined to the `primesec.local` Active Directory domain.

As a domain client, it uses `DC-01` for domain service discovery, Active Directory DNS resolution, and Group Policy processing.

### DHCP Client

`WS-01` receives its network configuration from `FW-01` through DHCP.

The observed dynamic lease for the workstation is `10.10.10.152`.

### Group Policy Target

`WS-01` processes computer Group Policy from `DC-01`.

Applied GPOs observed during validation include:

- `GPO-Workstation-Security-Baseline`
- `GPO-Workstation-Windows-Update`
- `GPO-Interactive-Logon-Notice`
- `GPO-Domain-Password-Policy`
- `Default Domain Policy`

### Interactive Logon Notice

The interactive logon notice is applied to `WS-01` through Group Policy and appears before sign-in.

---

## Related Documentation

| Document | Purpose |
| --- | --- |
| [WS-01 Validation](validation.md) | Validation evidence for workstation identity, domain integration, Group Policy processing, and the interactive logon notice |
| [DC-01 Group Policy](../dc-01/group-policy.md) | Implemented Group Policy configuration managed through `DC-01` |
| [FW-01 Validation](../fw-01/validation.md) | DHCP validation evidence for the observed `WS-01` lease |

---

## Validation Reference

`WS-01` validation is documented in [WS-01 Validation](validation.md).

Validation covers:

- Workstation identity
- Domain naming
- Computer Group Policy processing
- Applied Group Policy Objects
- Interactive logon notice application
- Dynamic DHCP lease reference
