# PrimeSec Infrastructure

PrimeSec Infrastructure is a hands-on infrastructure portfolio project focused on Systems Administration, networking, virtualization, Windows Server administration, Linux server administration, security hardening, validation, and technical documentation.

The project simulates a small business infrastructure environment using virtualized systems. Its purpose is to demonstrate practical junior-level infrastructure skills through real implementation work, documented design decisions, and validation evidence.

> This README is a correction pass for the current repository state. A final polished portfolio README can be produced after the remaining documentation cleanup is complete.

---

## Infrastructure Status

| Component | Role | Status |
|-----------|------|--------|
| FW-01 | OPNsense firewall, gateway, NAT, DHCP, remote access entry point | Complete |
| DC-01 | Windows Server 2022 Domain Controller, Active Directory, DNS, Group Policy | Complete |
| WS-01 | Windows domain-joined workstation | Complete |
| WEB-01 | Ubuntu Server 24.04.4 LTS with Apache HTTP Server | Complete |

---

## Architecture Overview

PrimeSec Infrastructure is deployed as a virtualized lab environment on Proxmox VE.

The current Phase 1 environment includes:

- A dedicated firewall and gateway layer
- A Windows Active Directory domain
- A managed Windows workstation
- A Linux-based Apache web server
- Validation screenshots and technical documentation for each major component

```text
                Internet / Upstream Network
                          │
                          ▼
                    ┌──────────┐
                    │  FW-01   │
                    │ OPNsense │
                    └────┬─────┘
                         │
                 Internal Network
                  10.10.10.0/24
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
   ┌────────┐       ┌────────┐       ┌────────┐
   │ DC-01  │       │ WS-01  │       │ WEB-01 │
   │ AD DS  │       │ Win WS │       │ Apache │
   │ DNS    │       │ Domain │       │ Ubuntu │
   └────────┘       └────────┘       └────────┘
```

### Diagram Note

The existing architecture diagram files are kept temporarily:

- `diagrams/v1-architecture.drawio`
- `diagrams/v1-architecture.png`

The diagram is pending update to fully reflect the completed DC-01 and WS-01 implementation. It has not been regenerated in this correction pass.

---

## Network and DNS Model

The final internal Active Directory namespace is:

```text
primesec.local
```

The current DNS model is:

| Function | System |
|----------|--------|
| Default gateway | FW-01 / 10.10.10.1 |
| DHCP ownership | FW-01 |
| Authoritative internal DNS for Active Directory | DC-01 / 10.10.10.10 |
| Active Directory domain namespace | primesec.local |
| Secure remote access entry point | FW-01 through Tailscale |

DHCP should provide the following client configuration:

| DHCP Option | Value |
|-------------|-------|
| Gateway | 10.10.10.1 |
| DNS Server | 10.10.10.10 |
| Domain/Search Suffix | primesec.local |
| DHCP Scope Range | 10.10.10.100 - 10.10.10.199 |

Older references to `primesec.internal` belong to previous lab naming and should not be treated as the current Active Directory DNS design.

---

## Technologies Used

- Proxmox VE
- OPNsense
- Tailscale
- Windows Server 2022
- Active Directory Domain Services
- Active Directory Integrated DNS
- Group Policy
- Windows Workstation
- Ubuntu Server 24.04.4 LTS
- Apache HTTP Server
- UFW
- Unattended security updates

---

## Skills Demonstrated

This project demonstrates practical skills relevant to junior Systems Administration, Infrastructure, and IT Operations roles:

- Virtualized infrastructure deployment
- Firewall administration
- Network routing and NAT
- DHCP planning
- DNS design and troubleshooting
- Active Directory deployment
- Organizational Unit design
- Group Policy configuration
- Domain-joined workstation management
- Linux server deployment
- Apache web service administration
- Host-based firewall configuration
- Secure remote administration
- System hardening
- Validation testing
- Technical documentation

---

## Documentation

### Architecture

- [Design Decisions](docs/architecture/design-decisions.md)

### Networking

- [DNS Configuration](docs/networking/dns.md)

### FW-01 — OPNsense Firewall

- [Overview](docs/fw-01/overview.md)
- [Hardening](docs/fw-01/hardening.md)
- [Tailscale Remote Access](docs/fw-01/tailscale.md)
- [Validation](docs/fw-01/validation.md)

### DC-01 — Windows Server Domain Controller

- [Overview](docs/dc-01/overview.md)
- [Group Policy](docs/dc-01/group-policy.md)
- [Validation](docs/dc-01/validation.md)

### WS-01 — Windows Workstation

- [Overview](docs/ws-01/overview.md)
- [Validation](docs/ws-01/validation.md)

### WEB-01 — Ubuntu Server

- [Overview](docs/web-01/overview.md)
- [Deployment](docs/web-01/web-01.md)
- [Hardening](docs/web-01/hardening.md)
- [Validation](docs/web-01/validation.md)
- [Design Decisions](docs/web-01/design-decisions.md)

---

## Validation Evidence

Validation evidence is stored under the `assets/` directory.

| Component | Evidence Folder |
|-----------|-----------------|
| FW-01 | `assets/fw-01/` |
| DC-01 | `assets/dc-01/` |
| WS-01 | `assets/ws-01/` |
| WEB-01 | `assets/web-01/` |

The evidence includes screenshots for connectivity, DNS resolution, service status, firewall configuration, Active Directory validation, Group Policy processing, domain membership, and web service availability.

---

## Repository Structure

```text
PrimeSec-Infrastructure/
│
├── README.md
├── diagrams/
│   ├── v1-architecture.drawio
│   └── v1-architecture.png
│
├── docs/
│   ├── architecture/
│   ├── dc-01/
│   ├── fw-01/
│   ├── networking/
│   ├── web-01/
│   └── ws-01/
│
├── assets/
│   ├── dc-01/
│   ├── fw-01/
│   ├── web-01/
│   └── ws-01/
│
└── reports/
    └── gpo/
```

---

## Current Progress

### Completed

- OPNsense firewall deployment
- Firewall hardening
- Tailscale remote administration
- DHCP ownership assigned to FW-01
- Active Directory Domain Services deployment
- Active Directory Integrated DNS deployment
- Group Policy configuration
- Windows workstation domain join
- Ubuntu Server deployment
- Apache web service deployment
- Linux host-based firewall configuration
- Component validation and evidence collection
- Technical documentation for Phase 1 components

### Pending Cleanup

- Update the architecture diagram to reflect the completed DC-01 and WS-01 implementation
- Continue documentation consistency review
- Produce final recruiter-facing README polish after the critical documentation issues are resolved

---

## Project Purpose

PrimeSec Infrastructure is not intended to represent a production enterprise environment.

It is a realistic junior/internship infrastructure portfolio project designed to demonstrate:

- Practical implementation ability
- Understanding of infrastructure components
- Documentation discipline
- Validation mindset
- Awareness of operational and security considerations

The project is suitable for review by instructors, internship recruiters, junior Systems Administration hiring managers, and technical interviewers.