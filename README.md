# PrimeSec Infrastructure

PrimeSec Infrastructure is a virtualized infrastructure lab focused on core systems administration tasks: firewalling, routing, NAT, DHCP, DNS, Active Directory, Group Policy, Linux web service hosting, remote administration, and validation.

The current Phase 1 environment represents a small internal network with one firewall, one domain controller, one domain-joined workstation, and one Linux web server.

This project is not intended to represent a production enterprise environment. It is a controlled lab used to build, document, and validate common infrastructure services.

> The architecture diagram still needs to be refreshed. The written documentation reflects the current Phase 1 implementation more accurately than the existing diagram.

---

## Phase 1 Status

| Component | Role | Status |
|-----------|------|--------|
| FW-01 | OPNsense firewall, gateway, NAT, DHCP, Tailscale remote access | Implemented |
| DC-01 | Windows Server 2022 Domain Controller, AD DS, DNS, Group Policy | Implemented |
| WS-01 | Windows 11 Enterprise domain-joined workstation | Implemented |
| WEB-01 | Ubuntu Server 24.04.4 LTS with Apache HTTP Server | Implemented |

---

## Architecture Overview

PrimeSec Infrastructure is deployed as a virtualized lab environment on Proxmox VE.

Current Phase 1 components:

- FW-01 provides firewalling, routing, NAT, DHCP, gateway services, and Tailscale-based remote administration.
- DC-01 provides Active Directory Domain Services, integrated DNS, and Group Policy.
- WS-01 is joined to the `primesec.local` domain and receives policy from DC-01.
- WEB-01 hosts a basic Apache web service on Ubuntu Server.

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
   │ AD DS  │       │ Win 11 │       │ Apache │
   │ DNS    │       │ Domain │       │ Ubuntu │
   └────────┘       └────────┘       └────────┘
```

### Diagram Note

The following diagram files are still present:

- `diagrams/v1-architecture.drawio`
- `diagrams/v1-architecture.png`

The diagram has not yet been updated to fully reflect the completed DC-01 and WS-01 implementation.

---

## Network and DNS Model

The current Active Directory namespace is:

```text
primesec.local
```

| Function | System |
|----------|--------|
| Default gateway | FW-01 / 10.10.10.1 |
| DHCP provider | FW-01 |
| Active Directory DNS authority | DC-01 / 10.10.10.10 |
| Active Directory domain | primesec.local |
| Remote administration entry point | FW-01 through Tailscale |

DHCP configuration:

| DHCP Option | Value |
|-------------|-------|
| Gateway | 10.10.10.1 |
| DNS Server | 10.10.10.10 |
| Domain/Search Suffix | primesec.local |
| DHCP Scope Range | 10.10.10.100 - 10.10.10.199 |

Verified DHCP lease:

| Item | Value |
|------|-------|
| Client | WS-01 |
| Lease Address | 10.10.10.152 |
| Lease Type | Dynamic |

---

## Technologies Used

- Proxmox VE
- OPNsense
- Tailscale
- Windows Server 2022
- Active Directory Domain Services
- Active Directory Integrated DNS
- Group Policy
- Windows 11 Enterprise
- Ubuntu Server 24.04.4 LTS
- Apache HTTP Server
- UFW
- Unattended security updates

---

## Technical Areas Covered

The current implementation covers:

- Virtual machine deployment
- Internal network segmentation
- Firewall and gateway configuration
- NAT and routing
- DHCP configuration and validation
- Active Directory deployment
- DNS design for a Windows domain
- Organizational Unit structure
- Group Policy configuration
- Domain-joined workstation management
- Linux server deployment
- Apache service administration
- Host-based firewall configuration
- Tailscale-based remote administration
- Service validation and documentation

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

The evidence includes screenshots for connectivity, DNS resolution, DHCP configuration, DHCP lease assignment, service status, firewall configuration, Active Directory validation, Group Policy processing, domain membership, and web service availability.

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

## Known Limitations

The architecture diagram has not yet been refreshed to fully match the completed Phase 1 environment.

The written documentation reflects the current implementation more accurately than the existing diagram.

---

## Project Scope

PrimeSec Infrastructure is a small infrastructure lab.

It focuses on building and validating a clear Phase 1 environment with:

- One firewall/gateway
- One Active Directory domain controller
- One managed Windows workstation
- One Linux web server
- Supporting documentation and validation evidence