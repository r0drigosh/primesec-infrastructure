# FW-01 Overview

## Purpose

FW-01 is the primary network gateway and security boundary of the PrimeSec Infrastructure environment.

It is responsible for routing traffic between the internal infrastructure network and upstream connectivity while providing core network services required by the lab environment.

FW-01 simulates the role of a dedicated firewall appliance commonly deployed in small and medium-sized environments. It provides practical experience in firewall administration, routing, NAT, DHCP, remote access, and infrastructure security.

---

## Platform Information

| Property | Value |
|----------|-------|
| Hostname | FW-01 |
| Platform | OPNsense |
| Virtualization Platform | Proxmox VE |
| Start at Boot | Enabled |

---

## Infrastructure Role

FW-01 serves as the central networking component of PrimeSec Infrastructure.

Current infrastructure systems relying on FW-01 include:

- DC-01 — Windows Server Domain Controller
- WS-01 — Windows domain-joined workstation
- WEB-01 — Ubuntu Server with Apache HTTP Server

Without FW-01, infrastructure systems would lose:

- Default gateway access
- Internet connectivity
- NAT
- DHCP services
- Firewall policy enforcement
- Secure remote administration through Tailscale

---

## Network Interfaces

FW-01 is configured with two network interfaces.

| Interface | Purpose |
|-----------|---------|
| WAN | External or upstream network connectivity |
| LAN | Internal infrastructure network |

The LAN interface acts as the default gateway for infrastructure systems.

### Internal Network

```text
10.10.10.0/24
```

### Default Gateway

```text
10.10.10.1
```

This design provides a simple and maintainable network architecture while keeping internal resources behind a dedicated firewall layer.

---

## Services Provided

FW-01 provides several foundational infrastructure services.

### Routing

FW-01 routes traffic between the internal infrastructure network and upstream connectivity.

### Network Address Translation

FW-01 provides NAT so systems using private internal addressing can access external resources.

### DHCP

FW-01 owns DHCP for the internal infrastructure network.

DHCP should provide clients with:

| Setting | Value |
|---------|-------|
| Default Gateway | 10.10.10.1 |
| DNS Server | 10.10.10.10 |
| Domain/Search Suffix | primesec.local |
| DHCP Scope Range | 10.10.10.100 - 10.10.10.199 |

The exact DHCP range is not verified in the current repository sources.

### Firewall Services

FW-01 enforces traffic filtering and network security controls between internal systems and upstream connectivity.

### Secure Remote Administration

FW-01 supports secure remote administration through Tailscale.

This allows administrative access without exposing management services directly to the public Internet.

---

## DNS Role Clarification

FW-01 is not the authoritative DNS server for the Active Directory domain.

The final internal Active Directory namespace is:

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
| [DNS Configuration](../networking/dns.md) | Final DNS and DHCP responsibility model |

---

## Skills Demonstrated

FW-01 demonstrates practical experience in:

- Firewall administration
- Network routing
- NAT
- DHCP ownership
- TCP/IP networking
- Infrastructure design
- Virtualization
- Secure remote access
- Security hardening
- Technical documentation
- Infrastructure validation

FW-01 provides the networking and security foundation required by the current Phase 1 PrimeSec Infrastructure environment.