# FW-01 Overview

## Purpose

FW-01 is the primary network gateway and security boundary of the PrimeSec Infrastructure environment.

It is responsible for routing traffic between internal and external networks while providing core network services required by all systems within the infrastructure.

The system was designed to simulate the role of a dedicated firewall appliance commonly deployed in small and medium-sized business environments, providing practical experience in networking, systems administration and infrastructure security.

---

## Platform Information

| Property | Value |
|-----------|---------|
| Hostname | FW-01 |
| Platform | OPNsense |
| Virtualization Platform | Proxmox VE |
| Start at Boot | Enabled |

### Virtualization

FW-01 operates as a dedicated virtual firewall appliance hosted on Proxmox VE.

The virtualized deployment provides flexibility, simplified management and an environment suitable for infrastructure testing, documentation and administration.

---

## Infrastructure Role

FW-01 serves as the central networking component of the PrimeSec Infrastructure environment.

All internal systems depend on FW-01 for connectivity, routing and access to external resources.

Current infrastructure dependencies include:

- WEB-01 (Ubuntu Server)
- DC-01 (Windows Server) *(planned)*
- WS-01 (Windows Workstation) *(planned)*

Without FW-01, infrastructure systems would lose:

- Internet connectivity
- Internal routing
- DHCP services
- Network security controls
- Secure remote administration

---

## Network Interfaces

FW-01 is configured with two network interfaces.

| Interface | Purpose |
|------------|---------|
| WAN | External network connectivity |
| LAN | Internal infrastructure network |

The LAN interface acts as the default gateway for all infrastructure systems.

### Internal Network

```text
10.10.10.0/24
```

### Default Gateway

```text
10.10.10.1
```

This design provides a simple and maintainable network architecture while maintaining separation between internal resources and external networks.

---

## Services Provided

FW-01 provides several foundational infrastructure services.

### Routing

Routes traffic between internal and external networks.

### Network Address Translation (NAT)

Allows internal systems using private IP addressing to access external resources.

### DHCP

Provides network configuration services for infrastructure devices when required.

### Firewall Services

Enforces network security policies and traffic filtering.

### Infrastructure Gateway

Acts as the default gateway for all connected systems.

### Secure Remote Administration

Supports secure administrative access through Tailscale integration.

Additional implementation details are documented within the dedicated FW-01 documentation set.

---

## Infrastructure Dependencies

FW-01 relies on the following components:

### Proxmox VE

Provides virtualization resources and virtual networking.

### Upstream Network Connectivity

Provides Internet access and external network reachability.

### Administrative Devices

Authorized management devices used for infrastructure administration and maintenance.

All remaining PrimeSec Infrastructure systems rely directly on FW-01 for communication and network services.

---

## Related Documentation

| Document | Description |
|-----------|-------------|
| hardening.md | Security controls and hardening measures applied to FW-01 |
| tailscale.md | Remote administration architecture and VPN integration |
| firewall-rules.md | Firewall policy documentation *(planned)* |
| validation.md | Operational testing and validation procedures *(planned)* |

---

## Skills Demonstrated

FW-01 demonstrates practical experience in:

- Firewall Administration
- Network Routing
- TCP/IP Networking
- Infrastructure Design
- Virtualization
- Secure Remote Access
- Security Hardening
- Technical Documentation
- Infrastructure Operations

FW-01 serves as the foundational infrastructure component of PrimeSec Infrastructure and provides the networking and security services required by all current and future Phase 1 systems.