# FW-01 Overview

## Purpose

`FW-01` is the OPNsense firewall for the PrimeSec Infrastructure environment.

It provides the internal gateway, NAT, DHCP, firewall policy enforcement, and Tailscale-based remote administration.

---

## Environment Role

`FW-01` is the network edge for the internal infrastructure network. It separates internal systems from upstream connectivity and provides the default route for the environment.

Systems behind `FW-01` include:

- `DC-01` — Windows Server 2022 domain controller
- `WS-01` — Windows 11 Pro domain-joined workstation
- `WEB-01` — Ubuntu Server Apache web server

---

## System Summary

| Property | Value |
| --- | --- |
| Component | `FW-01` |
| Platform | OPNsense |
| Virtualization Platform | Proxmox VE |
| Role | Firewall, gateway, NAT, DHCP, and remote access |

---

## Network Summary

| Property | Value |
| --- | --- |
| Internal Network | `10.10.10.0/24` |
| LAN Gateway | `10.10.10.1` |
| DHCP Scope | `10.10.10.100 - 10.10.10.199` |
| DHCP DNS Server | `DC-01` / `10.10.10.10` |
| DHCP Domain/Search Suffix | `primesec.local` |
| Remote Access | Tailscale |

`FW-01` provides DHCP for the internal network and distributes `DC-01` as the DNS server for domain clients.

`DC-01` remains authoritative for the `primesec.local` Active Directory namespace.

---

## Key Functions

### Gateway, Routing, and NAT

`FW-01` routes traffic between the internal network and upstream connectivity.

NAT allows systems on `10.10.10.0/24` to reach external resources through the firewall.

### DHCP

`FW-01` provides DHCP for the internal network.

The configured DHCP scope is `10.10.10.100 - 10.10.10.199`.

`WS-01` holds the observed dynamic lease `10.10.10.152`.

### Firewall Policy

`FW-01` applies network filtering between the internal infrastructure network and upstream connectivity.

### Remote Administration

`FW-01` uses Tailscale for remote administration.

This provides a remote management path without exposing the OPNsense management interface directly to the public Internet.

---

## Related Documentation

| Document | Purpose |
| --- | --- |
| [FW-01 Hardening](hardening.md) | Security controls applied to the firewall |
| [Tailscale Integration](tailscale.md) | Tailscale remote access and subnet routing |
| [FW-01 Validation](validation.md) | Validation evidence for FW-01 functions |

---

## Validation Reference

`FW-01` validation is documented in [FW-01 Validation](validation.md).

Validation covers:

- Interface assignments
- External connectivity
- External DNS resolution from `FW-01`
- DHCP scope configuration
- `WS-01` dynamic DHCP lease assignment
- Tailscale-based Web GUI reachability
