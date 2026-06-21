# Architecture Design Decisions

## Purpose

This document records the main architecture decisions used in the PrimeSec Infrastructure environment.

The goal is to keep the cross-component design readable without repeating every implementation detail from the component documentation.

---

## Architecture Scope

PrimeSec Infrastructure is a compact virtualized infrastructure lab built around a small internal network, a dedicated firewall, a Windows domain, a managed Windows workstation, and an internal Linux web server.

| Component | Role |
| --- | --- |
| `FW-01` | Firewall, gateway, NAT, DHCP, and Tailscale remote access |
| `DC-01` | Windows Server domain controller, Active Directory, DNS, and Group Policy |
| `WS-01` | Windows 11 Pro domain-joined workstation |
| `WEB-01` | Ubuntu Server Apache web server |

---

## Design Principles

The environment uses a small number of clearly separated components.

The design follows these principles:

- Keep routing, DHCP, firewalling, and remote access on `FW-01`.
- Keep Active Directory, domain DNS, and Group Policy on `DC-01`.
- Use `WS-01` as the managed Windows client and Group Policy target.
- Use `WEB-01` as a simple internal Linux service.
- Keep validation evidence close to the component it validates.
- Avoid mixing documentation for unrelated roles into the same component file.

---

## Virtualized Infrastructure

The environment runs as a virtualized lab on Proxmox VE.

Virtualization keeps each infrastructure role separated while allowing the full environment to run on a single host. This supports snapshot-based recovery, repeatable testing, and isolated lab networking.

---

## Network Edge

`FW-01` is the central network edge for the lab.

It provides:

- Default gateway services
- Routing
- NAT
- DHCP
- Firewall policy enforcement
- Tailscale-based remote administration

| Item | Value |
| --- | --- |
| Internal network | `10.10.10.0/24` |
| Default gateway | `FW-01` / `10.10.10.1` |
| DHCP provider | `FW-01` |
| DHCP scope | `10.10.10.100 - 10.10.10.199` |

Keeping these functions on the firewall keeps network edge responsibilities separate from Windows domain services.

---

## Identity and DNS

`DC-01` provides the Windows domain and the authoritative internal DNS namespace for Active Directory.

| Item | Value |
| --- | --- |
| Domain | `primesec.local` |
| NetBIOS name | `PRIMESEC` |
| Domain controller | `DC-01` |
| Domain controller IP | `10.10.10.10` |
| DNS model | Active Directory Integrated DNS |

Domain-joined systems use `DC-01` for Active Directory service discovery, internal domain name resolution, and Group Policy processing.

---

## DHCP Ownership

DHCP is provided by `FW-01` instead of `DC-01`.

This keeps addressing, gateway assignment, and network edge services on the firewall while still directing domain clients to the Active Directory DNS server.

| DHCP value | Setting |
| --- | --- |
| Gateway | `10.10.10.1` |
| DNS server | `10.10.10.10` |
| DNS namespace | `primesec.local` |
| Scope range | `10.10.10.100 - 10.10.10.199` |

The observed `WS-01` dynamic lease is `10.10.10.152`.

---

## Windows Workstation

`WS-01` is the managed Windows workstation in the environment.

It is joined to `primesec.local`, receives DHCP configuration from `FW-01`, and processes computer Group Policy from `DC-01`.

| Item | Value |
| --- | --- |
| Component | `WS-01` |
| Operating system | Windows 11 Pro |
| Domain | `primesec.local` |
| Observed DHCP lease | `10.10.10.152` |
| Lease type | `dynamic` |

`WS-01` validates workstation-side domain integration and policy application without duplicating the full Group Policy configuration, which is documented under `DC-01`.

---

## Linux Web Server

`WEB-01` provides a basic internal Linux-hosted Apache service.

| Item | Value |
| --- | --- |
| Component | `WEB-01` |
| Operating system | Ubuntu Server 24.04.4 LTS |
| Primary service | Apache HTTP Server |
| IP address | `10.10.10.11` |

The web server scope is intentionally limited to host configuration, Apache service operation, host firewall state, and internal reachability.

---

## Remote Administration

Remote administration is provided through Tailscale on `FW-01`.

This provides a controlled management path without exposing the firewall management interface directly to the public Internet.

---

## Group Policy

Group Policy is managed through `DC-01` and applied to the domain environment.

Implemented GPOs include:

- `GPO-Domain-Password-Policy`
- `GPO-Interactive-Logon-Notice`
- `GPO-Workstation-Security-Baseline`
- `GPO-Workstation-Windows-Update`

Detailed Group Policy configuration is documented in [DC-01 Group Policy](../dc-01/group-policy.md). Exported reports are stored under [Group Policy Reports](../../reports/gpo/).

---

## Documentation Model

The repository is organized around the main infrastructure components.

| Area | Purpose |
| --- | --- |
| `README.md` | Project entry point and high-level summary |
| `docs/fw-01/` | Firewall, DHCP, NAT, validation, and Tailscale documentation |
| `docs/dc-01/` | Active Directory, DNS, Group Policy, and validation documentation |
| `docs/ws-01/` | Windows workstation and Group Policy application validation |
| `docs/web-01/` | Linux web server configuration, hardening, and validation |
| `docs/architecture/` | Cross-component architecture decisions |
| `assets/` | Validation screenshots grouped by component |
| `reports/gpo/` | Exported Group Policy reports |

Validation evidence remains in component-specific validation files instead of being duplicated in the architecture document.

---

## Related Documentation

| Document | Purpose |
| --- | --- |
| [README](../../README.md) | Project overview and navigation |
| [Architecture diagram](../../diagrams/architecture.png) | Current lab topology diagram |
| [Diagram source](../../diagrams/architecture.drawio) | Editable Draw.io diagram source |
| [FW-01 Overview](../fw-01/overview.md) | Firewall and network edge role |
| [DC-01 Overview](../dc-01/overview.md) | Domain controller, DNS, and Group Policy role |
| [WS-01 Overview](../ws-01/overview.md) | Windows workstation role |
| [WEB-01 Overview](../web-01/overview.md) | Internal Linux web server role |

---

## Design Summary

The environment uses `FW-01` as the network edge, `DC-01` as the identity and DNS authority, `WS-01` as the managed Windows workstation, and `WEB-01` as the internal Linux web server.

This keeps each component focused, documented, and validated through its own evidence set.
