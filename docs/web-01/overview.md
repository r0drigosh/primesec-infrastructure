# WEB-01 Overview

## Purpose

WEB-01 is the Linux-based web server component of the PrimeSec Infrastructure environment.

Its primary purpose is to provide a practical platform for demonstrating core Systems Administration skills, including Linux server deployment, network configuration, service management, security hardening and infrastructure documentation.

The server hosts a simple Apache web page used to validate service availability and demonstrate successful deployment of a web service within the lab environment.

---

## Platform Information

| Property | Value |
|-----------|---------|
| Hostname | web-01 |
| Operating System | Ubuntu Server 24.04.4 LTS |
| Platform Type | Virtual Machine |
| Virtualization Platform | Proxmox VE |
| Primary Service | Apache HTTP Server |
| Network Configuration | Static IP Address |
| Firewall | UFW (Uncomplicated Firewall) |
| Automatic Security Updates | Enabled |

### System Purpose

WEB-01 was deployed as a dedicated Linux server to provide hands-on experience with common server administration tasks and service management activities frequently encountered in entry-level Systems Administration and Infrastructure roles.

---

## Infrastructure Role

WEB-01 functions as the dedicated web server within the PrimeSec Infrastructure environment.

The system provides a hosted web service that can be accessed from the internal network and serves as a platform for validating:

- Linux server administration
- Static network configuration
- Service deployment and management
- Host-based firewall configuration
- Infrastructure security hardening
- Network connectivity

Within the Phase 1 architecture, WEB-01 operates behind FW-01 and relies on the firewall for network routing, DNS resolution and access to external resources.

---

## Services Provided

WEB-01 currently provides the following infrastructure services:

### Web Hosting

Hosts a lightweight Apache web page used for service validation and infrastructure testing.

### HTTP Service

Provides HTTP connectivity to clients within the PrimeSec Infrastructure environment.

### Linux Administration Platform

Serves as a dedicated Linux server for demonstrating operating system management, service administration and security configuration.

### Infrastructure Validation

Provides a testable service endpoint used to verify network connectivity, routing and firewall functionality throughout the environment.

---

## Infrastructure Dependencies

WEB-01 depends on the following infrastructure components:

### FW-01 (OPNsense Firewall)

Provides:

- Default gateway services
- Network routing
- Internet access
- DNS forwarding and resolution
- Network security controls

### Proxmox VE

Provides:

- Virtualization resources
- Virtual networking
- Storage allocation
- Virtual machine lifecycle management

### Internal Network

WEB-01 operates within the PrimeSec Infrastructure network and relies on internal network connectivity for communication with current and future infrastructure systems.

Planned Phase 1 integrations include:

- DC-01 (Windows Server)
- WS-01 (Windows Workstation)

---

## Related Documentation

| Document | Description |
|-----------|-------------|
| web-01.md | Deployment and configuration procedures |
| hardening.md | Security hardening measures applied to WEB-01 |
| validation.md | Operational testing and validation results |
| design-decisions.md | Architectural decisions and implementation rationale |

---

## Skills Demonstrated

WEB-01 demonstrates practical experience in:

- Linux Server Administration
- Ubuntu Server Deployment
- Static IP Configuration
- Hostname Management
- Apache Web Server Administration
- Service Management with systemd
- SSH Administration
- Network Troubleshooting
- DNS Validation
- Host-Based Firewall Configuration (UFW)
- Linux Security Hardening
- Automatic Security Update Management
- Infrastructure Documentation
- Virtualization Fundamentals
- Systems Validation and Testing

WEB-01 provides a practical example of a managed Linux infrastructure service and demonstrates the foundational administration skills expected in junior Systems Administration, Infrastructure and IT Operations roles.