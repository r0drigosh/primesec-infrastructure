# WS-01 Overview

## Purpose

`WS-01` is the managed Windows workstation in the PrimeSec Infrastructure environment.

It runs Windows 11 Pro, is joined to the `primesec.local` domain, and receives workstation configuration through Active Directory Group Policy.

---

## Environment Role

`WS-01` represents a standard domain-joined client system on the internal network.

It is used to validate normal workstation integration with the domain, including authentication, DNS dependency, DHCP assignment, Group Policy processing, and the interactive logon notice.

---

## System Summary

| Property | Value |
| -------- | -------- |
| Component | `WS-01` |
| Operating System | Windows 11 Pro |
| Virtualization Platform | Proxmox VE |
| Role | Domain-joined workstation |

---

## Network Summary

| Property | Value |
| -------- | -------- |
| Network | `10.10.10.0/24` |
| DHCP Lease | `10.10.10.152` |
| Default Gateway | `FW-01` / `10.10.10.1` |
| DNS Server | `DC-01` / `10.10.10.10` |

`WS-01` receives its address dynamically from the `FW-01` DHCP scope `10.10.10.100 - 10.10.10.199`.

The address `10.10.10.152` is the observed DHCP lease for `WS-01`, not a static workstation address.

---

## Key Functions

### Domain Membership

`WS-01` is joined to the `primesec.local` Active Directory domain.

As a domain member, it uses `DC-01` for domain authentication, Active Directory service discovery, DNS resolution for the AD domain, and Group Policy processing.

### DHCP Client Configuration

`WS-01` receives its network configuration from `FW-01` through DHCP.

The documented lease confirms that `WS-01` received an address from the configured DHCP scope.

### Group Policy Processing

`WS-01` receives workstation configuration from Group Policy.

Validated applied policies include:

- `GPO-Workstation-Security-Baseline`
- `GPO-Workstation-Windows-Update`
- `GPO-Interactive-Logon-Notice`
- `GPO-Domain-Password-Policy`
- `Default Domain Policy`

### Interactive Logon Notice

The interactive logon notice is applied to `WS-01` through Group Policy and appears before user sign-in.

---

## Related Documentation

| Document | Purpose |
| -------- | -------- |
| [WS-01 Validation](validation.md) | Validation evidence for domain membership and policy application |
| [DC-01 Group Policy](../dc-01/group-policy.md) | Group Policy configuration applied to the workstation |
| [DNS Configuration](../networking/dns.md) | DNS and DHCP model used by domain clients |
| [FW-01 Validation](../fw-01/validation.md) | DHCP evidence for the WS-01 lease |

---

## Validation Reference

`WS-01` validation is documented in [WS-01 Validation](validation.md).

Validation covers:

- Domain membership
- Domain user authentication
- Group Policy processing
- Interactive logon notice application
- DHCP lease assignment