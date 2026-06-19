# FW-01 Overview

## Purpose

FW-01 is the firewall and default gateway for the PrimeSec Infrastructure environment.

It routes traffic between the internal infrastructure network and upstream connectivity, provides NAT, owns DHCP for the LAN, and provides a Tailscale-based remote administration path.

---

## Platform Information

| Property | Value |
|----------|-------|
| Hostname | FW-01 |
| Platform | OPNsense |
| Virtualization Platform | Proxmox VE |
| LAN IP Address | 10.10.10.1 |
| Start at Boot | Enabled |

---

## Infrastructure Role

FW-01 is the central network component for the Phase 1 environment.

Current systems depending on FW-01:

- DC-01 — Windows Server Domain Controller
- WS-01 — Windows 11 Enterprise domain-joined workstation
- WEB-01 — Ubuntu Server with Apache HTTP Server

FW-01 provides these core network functions:

- Default gateway access
- Routing
- NAT
- DHCP services
- Firewall policy enforcement
- Remote administration through Tailscale

---

## Network Interfaces

FW-01 is configured with two network interfaces.

| Interface | Purpose |
|-----------|---------|
| WAN | External or upstream network connectivity |
| LAN | Internal infrastructure network |

The LAN interface is the default gateway for the internal network.

### Internal Network

```text
10.10.10.0/24
```

### Default Gateway

```text
10.10.10.1
```

---

## Services Provided

### Routing

FW-01 routes traffic between the internal infrastructure network and the upstream network.

### Network Address Translation

FW-01 provides NAT so systems using private internal addressing can access external resources.

### DHCP

FW-01 owns DHCP for the internal infrastructure network.

DHCP is configured to provide clients with:

| Setting | Value |
|---------|-------|
| Default Gateway | 10.10.10.1 |
| DNS Server | 10.10.10.10 |
| Domain/Search Suffix | primesec.local |
| DHCP Scope Range | 10.10.10.100 - 10.10.10.199 |

Validation evidence shows that WS-01 received a dynamic DHCP lease from FW-01.

| Item | Verified Value |
|------|----------------|
| Client Hostname | WS-01 |
| Lease Address | 10.10.10.152 |
| Lease Type | Dynamic |

### Firewall Services

FW-01 applies traffic filtering between the internal network and upstream connectivity.

### Remote Administration

FW-01 is reachable for administration through Tailscale.

This avoids exposing the OPNsense management interface directly to the public Internet.

---

## DNS Role Clarification

FW-01 is not the authoritative DNS server for the Active Directory domain.

The current Active Directory namespace is:

```text
primesec.local
```

The authoritative internal DNS server for Active Directory and domain-joined systems is:

```text
DC-01 / 10.10.10.10
```

FW-01 may provide upstream or external DNS forwarding for non-domain or network-level services, but Active Directory DNS authority belongs to DC-01.

Older references to `primesec.internal` or FW-01 as the primary internal AD DNS server should be treated as legacy lab naming.

---

## Infrastructure Dependencies

FW-01 relies on the following components.

### Proxmox VE

Provides:

- Virtualization resources
- Virtual networking
- Virtual machine lifecycle management

### Upstream Network Connectivity

Provides:

- Internet access
- External network reachability
- Connectivity required for updates and external DNS testing

### Administrative Devices

Authorized administrative devices are used to manage FW-01 through approved access paths, including Tailscale-based remote administration.

---

## Related Documentation

| Document | Description |
|----------|-------------|
| [Hardening](hardening.md) | Security controls and hardening measures applied to FW-01 |
| [Tailscale Remote Access](tailscale.md) | Remote administration architecture and VPN integration |
| [Validation](validation.md) | Operational testing and validation evidence |
| [DNS Configuration](../networking/dns.md) | DNS and DHCP responsibility model |

---

## Summary

FW-01 provides the network edge for the current Phase 1 environment.

It is responsible for gateway services, routing, NAT, DHCP, firewalling, and Tailscale-based remote administration.