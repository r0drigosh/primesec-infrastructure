# PrimeSec Infrastructure

![Status](https://img.shields.io/badge/Status-Validated%20Lab-lightgrey) ![Platform](https://img.shields.io/badge/Platform-Proxmox%20VE-lightgrey) ![Firewall](https://img.shields.io/badge/Firewall-OPNsense-lightgrey) ![Identity](https://img.shields.io/badge/Identity-AD%20DS-lightgrey) ![Web](https://img.shields.io/badge/Web-Apache-lightgrey)

PrimeSec Infrastructure is a virtualized infrastructure lab focused on core systems administration and infrastructure validation.

The current implementation contains an internal network with an OPNsense firewall, a Windows Server domain controller, a domain-joined Windows workstation, and an Ubuntu Apache web server. The repository includes component documentation, validation screenshots, and exported Group Policy reports.

---

## Current Implementation

| Component | Role                                                       | Key Details                                                        | Docs                            | Evidence                 |
| --------- | ---------------------------------------------------------- | ------------------------------------------------------------------ | ------------------------------- | ------------------------ |
| FW-01     | Firewall, gateway, NAT, DHCP, Tailscale remote access      | LAN gateway `10.10.10.1`; DHCP scope `10.10.10.100 - 10.10.10.199` | [Docs](docs/fw-01/overview.md)  | [Assets](assets/fw-01/)  |
| DC-01     | Windows Server domain controller, AD DS, DNS, Group Policy | Domain `primesec.local`; IP `10.10.10.10`; NetBIOS `PRIMESEC`      | [Docs](docs/dc-01/overview.md)  | [Assets](assets/dc-01/)  |
| WS-01     | Domain-joined Windows workstation                          | Domain member; dynamic DHCP lease `10.10.10.152`                   | [Docs](docs/ws-01/overview.md)  | [Assets](assets/ws-01/)  |
| WEB-01    | Ubuntu Apache web server                                   | Static IP `10.10.10.11`; Apache HTTP Server; UFW enabled           | [Docs](docs/web-01/overview.md) | [Assets](assets/web-01/) |

---

## Quick Navigation

| Area             | Links                                                                                                                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Architecture     | [Design Decisions](docs/architecture/design-decisions.md) · [Diagram PNG](diagrams/v1-architecture.png) · [Diagram Source](diagrams/v1-architecture.drawio)                                                       |
| Networking       | [DNS Configuration](docs/networking/dns.md)                                                                                                                                                                       |
| Firewall         | [Overview](docs/fw-01/overview.md) · [Hardening](docs/fw-01/hardening.md) · [Tailscale](docs/fw-01/tailscale.md) · [Validation](docs/fw-01/validation.md)                                                         |
| Active Directory | [Overview](docs/dc-01/overview.md) · [Group Policy](docs/dc-01/group-policy.md) · [Validation](docs/dc-01/validation.md)                                                                                          |
| Workstation      | [Overview](docs/ws-01/overview.md) · [Validation](docs/ws-01/validation.md)                                                                                                                                       |
| Web Server       | [Overview](docs/web-01/overview.md) · [Deployment](docs/web-01/web-01.md) · [Hardening](docs/web-01/hardening.md) · [Validation](docs/web-01/validation.md) · [Design Decisions](docs/web-01/design-decisions.md) |
| Reports          | [Group Policy Reports](reports/gpo/)                                                                                                                                                                              |

---

## Architecture Overview

The environment is deployed as a virtualized lab on Proxmox VE.

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
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        ▼                  ▼                  ▼
   ┌──────────┐       ┌──────────┐       ┌──────────┐
   │  DC-01   │       │  WS-01   │       │  WEB-01  │
   │ AD DS    │       │ Win 11   │       │ Ubuntu   │
   │ DNS/GPO  │       │ Domain   │       │ Apache   │
   └──────────┘       └──────────┘       └──────────┘
```

Architecture files are stored under:

```text
diagrams/
├── v1-architecture.drawio
└── v1-architecture.png
```

---

## Network and DNS Model

| Function                       | System                  |
| ------------------------------ | ----------------------- |
| Internal network               | `10.10.10.0/24`         |
| Default gateway                | FW-01 / `10.10.10.1`    |
| DHCP provider                  | FW-01                   |
| Active Directory DNS authority | DC-01 / `10.10.10.10`   |
| Active Directory domain        | `primesec.local`        |
| Remote access                  | FW-01 through Tailscale |

DHCP is configured to provide clients with the following values:

| DHCP Option          | Value                         |
| -------------------- | ----------------------------- |
| Gateway              | `10.10.10.1`                  |
| DNS Server           | `10.10.10.10`                 |
| Domain/Search Suffix | `primesec.local`              |
| DHCP Scope Range     | `10.10.10.100 - 10.10.10.199` |

Verified DHCP lease:

| Item          | Value          |
| ------------- | -------------- |
| Client        | WS-01          |
| Lease Address | `10.10.10.152` |
| Lease Type    | Dynamic        |

---

## Validation Evidence

Validation evidence is stored under the `assets/` directory and referenced from the component validation documents.

| Component | Validation                                     | Evidence Includes                                                                                                 |
| --------- | ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| FW-01     | [FW-01 Validation](docs/fw-01/validation.md)   | Internet connectivity, DNS resolution, DHCP configuration, DHCP lease assignment, Tailscale remote access         |
| DC-01     | [DC-01 Validation](docs/dc-01/validation.md)   | Active Directory domain validation, OU structure, DNS forward lookup zone, DCDIAG, Group Policy linking           |
| WS-01     | [WS-01 Validation](docs/ws-01/validation.md)   | Domain membership, Group Policy processing, interactive logon notice                                              |
| WEB-01    | [WEB-01 Validation](docs/web-01/validation.md) | Network connectivity, DNS resolution, Apache service status, UFW firewall state, service startup, web page access |

Exported Group Policy reports are stored under:

```text
reports/gpo/
```

---

## Technologies Used

* Proxmox VE
* OPNsense
* Tailscale
* Windows Server 2022
* Active Directory Domain Services
* Active Directory Integrated DNS
* Group Policy
* Windows 11 Enterprise
* Ubuntu Server 24.04.4 LTS
* Apache HTTP Server
* UFW
* Unattended security updates

---

## Implemented Technical Areas

The current implementation covers:

* Virtual machine deployment
* Internal network segmentation
* Firewall and gateway configuration
* NAT and routing
* DHCP configuration and validation
* Active Directory deployment
* DNS design for a Windows domain
* Organizational Unit structure
* Group Policy configuration
* Domain-joined workstation management
* Linux server deployment
* Apache service administration
* Host-based firewall configuration
* Tailscale-based remote access
* Service validation and documentation

---

## Repository Structure

```text
PrimeSec-Infrastructure/
├── README.md
├── diagrams/
│   ├── v1-architecture.drawio
│   └── v1-architecture.png
├── docs/
│   ├── architecture/
│   ├── dc-01/
│   ├── fw-01/
│   ├── networking/
│   ├── web-01/
│   └── ws-01/
├── assets/
│   ├── dc-01/
│   ├── fw-01/
│   ├── web-01/
│   └── ws-01/
└── reports/
    └── gpo/
```

---

## Scope and Limitations

PrimeSec Infrastructure is a controlled lab environment, not a production enterprise deployment.

The current scope contains:

* One firewall/gateway
* One Active Directory domain controller
* One managed Windows workstation
* One Linux Apache web server
* Supporting documentation and validation evidence

Architecture files are included under `diagrams/`. Detailed component configuration and validation evidence are documented under `docs/` and `assets/`.

WEB-01 provides a basic Apache service for infrastructure validation. It is not intended to represent a full web application platform.
