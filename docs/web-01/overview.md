# WEB-01 Overview

## Purpose

WEB-01 is the Linux-based web server component of the PrimeSec Infrastructure environment.

Its primary purpose is to provide a practical platform for demonstrating core Systems Administration skills, including Linux server deployment, network configuration, service management, security hardening, validation, and technical documentation.

The server hosts a simple Apache web page used to validate service availability and demonstrate successful deployment of a web service within the lab environment.

---

## Platform Information

| Property | Value |
|----------|-------|
| Hostname | web-01 |
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

WEB-01 functions as the dedicated Linux web server within the PrimeSec Infrastructure environment.

The system provides a hosted web service that can be accessed from the internal network and serves as a platform for validating:

- Linux server administration
- Static network configuration
- Apache service deployment
- Service management with systemd
- Host-based firewall configuration
- Network connectivity
- DNS resolution
- Infrastructure security hardening

WEB-01 operates behind FW-01 and is part of the internal infrastructure network.

---

## Services Provided

WEB-01 currently provides the following infrastructure services.

### Web Hosting

Hosts a lightweight Apache landing page used for service validation and infrastructure testing.

### HTTP Service

Provides HTTP connectivity to clients within the PrimeSec Infrastructure environment.

### Linux Administration Platform

Serves as a dedicated Linux server for demonstrating operating system management, service administration, and security configuration.

### Infrastructure Validation Endpoint

Provides a testable service endpoint used to verify network connectivity, routing, firewall behavior, and web service availability.

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

The internal default gateway is `10.10.10.1`.

### DC-01 — Active Directory DNS

DC-01 is the authoritative internal DNS server for the `primesec.local` Active Directory domain.

The internal DNS authority is `10.10.10.10`.

For the final DNS model, systems that need to resolve internal `primesec.local` records should use DC-01 as the internal DNS authority.

### Proxmox VE

Proxmox VE provides:

- Virtualization resources
- Virtual networking
- Storage allocation
- Virtual machine lifecycle management

### Internal Network

WEB-01 operates within the PrimeSec Infrastructure internal network: `10.10.10.0/24`.

WEB-01 uses the static IP address `10.10.10.11`.

---

## DNS Model Note

Earlier documentation described WEB-01 as relying on FW-01 for DNS resolution.

The final project DNS model is now:

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
| [DNS Configuration](../networking/dns.md) | Final DNS model for the infrastructure |

---

## Skills Demonstrated

WEB-01 demonstrates practical experience in:

- Linux server administration
- Ubuntu Server deployment
- Static IP configuration
- Hostname management
- Apache web server administration
- Service management with systemd
- SSH administration
- Network troubleshooting
- DNS validation
- Host-based firewall configuration with UFW
- Linux security hardening
- Automatic security update management
- Infrastructure documentation
- Virtualization fundamentals
- Systems validation and testing

WEB-01 provides a practical example of a managed Linux infrastructure service and demonstrates foundational administration skills expected in junior Systems Administration, Infrastructure, and IT Operations roles.