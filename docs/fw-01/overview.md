# FW-01 Overview

## Purpose

`FW-01` is the OPNsense firewall for the PrimeSec Infrastructure environment.

It provides the internal network gateway, routing, NAT, DHCP, firewall policy enforcement, and Tailscale-based remote administration.

---

## Environment Role

`FW-01` is the network edge for the internal infrastructure network. It separates the lab network from upstream connectivity and provides the default route used by the internal systems.

Systems behind `FW-01` include:

- `DC-01` — Windows Server 2022 domain controller
- `WS-01` — Windows 11 Pro domain-joined workstation
- `WEB-01` — Ubuntu Server Apache web server

---

## System Summary

| Property | Value |
| -------- | -------- |
| Component | `FW-01` |
| Platform | OPNsense |
| Virtualization Platform | Proxmox VE |
| Role | Firewall, gateway, NAT, DHCP, and remote access |

---

## Network Summary

| Property | Value |
| -------- | -------- |
| Internal Network | `10.10.10.0/24` |
| Default Gateway | `10.10.10.1` |
| Active Directory DNS | `DC-01` / `10.10.10.10` |
| DHCP Scope | `10.10.10.100 - 10.10.10.199` |

`FW-01` provides DHCP for the internal network and uses `DC-01` as the DNS authority for Active Directory name resolution.

---

## Key Functions

### Gateway, Routing, and NAT

`FW-01` routes traffic between the internal network and upstream connectivity.

NAT allows internal systems using the `10.10.10.0/24` network to reach external resources through `FW-01`.

### DHCP

`FW-01` owns DHCP for the internal network.

DHCP is configured with:

- Scope: `10.10.10.100 - 10.10.10.199`
- Default gateway: `10.10.10.1`
- DNS server: `10.10.10.10`
- Domain/search suffix: `primesec.local`

`WS-01` currently holds a dynamic DHCP lease at `10.10.10.152`.

### Firewall Policy

`FW-01` applies network filtering between the internal infrastructure network and upstream connectivity.

### Remote Administration

`FW-01` provides remote administrative access through Tailscale. The Tailscale configuration is documented separately in the FW-01 Tailscale documentation.

---

## Related Documentation

| Document | Purpose |
| -------- | -------- |
| [FW-01 Hardening](hardening.md) | Security controls applied to the firewall |
| [Tailscale Integration](tailscale.md) | Tailscale remote access configuration |
| [DNS Configuration](../networking/dns.md) | DNS and DHCP responsibility model |
| [FW-01 Validation](validation.md) | Validation evidence for FW-01 functions |

---

## Validation Reference

`FW-01` validation is documented in [FW-01 Validation](validation.md).

Validation covers:

- External network connectivity
- External DNS resolution from `FW-01`
- DHCP scope configuration
- `WS-01` dynamic DHCP lease assignment
- Tailscale-based remote administration