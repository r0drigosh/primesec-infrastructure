# WEB-01 Overview

## Purpose

WEB-01 is the Linux web server in the PrimeSec Infrastructure environment.

It runs Ubuntu Server and Apache HTTP Server. The server hosts a simple web page used to validate network connectivity, service availability, firewall configuration, and Linux server administration tasks.

---

## Platform Information

| Property | Value |
|----------|-------|
| Hostname | WEB-01 |
| Operating System | Ubuntu Server 24.04.4 LTS |
| Platform Type | Virtual Machine |
| Virtualization Platform | Proxmox VE |
| Primary Service | Apache HTTP Server |
| Network Configuration | Static IP Address |
| Static IP Address | 10.10.10.11 |
| Default Gateway | FW-01 / 10.10.10.1 |
| Internal AD DNS Authority | DC-01 / 10.10.10.10 |
| Internal Domain Namespace | primesec.local |
| Firewall | UFW |
| Automatic Security Updates | Enabled |

---

## Infrastructure Role

WEB-01 provides a Linux-based service inside the internal infrastructure network.

The system is used to validate:

- Ubuntu Server deployment
- Static network configuration
- Apache service operation
- Service management with systemd
- Host-based firewall rules with UFW
- Network connectivity
- DNS resolution
- Basic Linux hardening steps

WEB-01 operates behind FW-01 on the internal network.

---

## Services Provided

### Web Hosting

WEB-01 hosts a lightweight Apache landing page for service validation.

### HTTP Service

WEB-01 provides HTTP access from the internal network.

### Linux Server Administration

WEB-01 is used for Linux administration tasks such as package management, service control, firewall configuration, hostname validation, and update configuration.

### Validation Endpoint

WEB-01 provides a testable service endpoint for checking routing, firewall behavior, DNS resolution, and web service availability.

---

## Infrastructure Dependencies

WEB-01 depends on the following infrastructure components.

### FW-01 — OPNsense Firewall

FW-01 provides:

- Default gateway services
- Network routing
- NAT
- Internet access
- Network security controls

The internal default gateway is:

```text
10.10.10.1
```

### DC-01 — Active Directory DNS

DC-01 is the authoritative internal DNS server for the `primesec.local` Active Directory domain.

The internal DNS authority is:

```text
10.10.10.10
```

Systems that need to resolve internal `primesec.local` records should use DC-01 as the internal DNS authority.

### Proxmox VE

Proxmox VE provides:

- Virtualization resources
- Virtual networking
- Storage allocation
- Virtual machine lifecycle management

### Internal Network

WEB-01 operates within the internal network:

```text
10.10.10.0/24
```

WEB-01 uses the static IP address:

```text
10.10.10.11
```

---

## DNS Model Note

Earlier documentation described WEB-01 as relying on FW-01 for DNS resolution.

The current DNS model is:

| Function | System |
|----------|--------|
| Active Directory DNS authority | DC-01 / 10.10.10.10 |
| Internal namespace | primesec.local |
| Default gateway | FW-01 / 10.10.10.1 |
| DHCP ownership | FW-01 |
| WEB-01 static IP address | 10.10.10.11 |

FW-01 may still provide upstream or external DNS forwarding for non-domain or network-level services, but it is not the authoritative DNS server for the Active Directory domain.

---

## Related Documentation

| Document | Description |
|----------|-------------|
| [Deployment](web-01.md) | WEB-01 deployment and configuration overview |
| [Hardening](hardening.md) | Security hardening measures applied to WEB-01 |
| [Validation](validation.md) | Operational testing and validation results |
| [Design Decisions](design-decisions.md) | Architectural decisions and implementation rationale |
| [DNS Configuration](../networking/dns.md) | DNS model for the infrastructure |

---

## Summary

WEB-01 is a static-IP Ubuntu Server running Apache HTTP Server on the internal network.

It provides a basic Linux service for testing connectivity, DNS resolution, firewall configuration, service startup, and web access within the Phase 1 environment.