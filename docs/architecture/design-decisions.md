# Architecture Design Decisions

## Purpose

This document records the main architecture decisions used in the PrimeSec Infrastructure environment.

The goal is to explain why the current Phase 1 lab is structured in this way and to keep the technical reasoning visible in the repository.

The design is intentionally small. It focuses on practical implementation, clear responsibilities, and a manageable infrastructure scope.

---

## Current Architecture Scope

The current Phase 1 environment includes the following systems:

| System | Role | Status |
|--------|------|--------|
| FW-01 | Firewall, gateway, NAT, DHCP, Tailscale remote access | Complete |
| DC-01 | Windows Server Domain Controller, Active Directory, DNS, Group Policy | Complete |
| WS-01 | Windows 11 Pro domain-joined workstation | Complete |
| WEB-01 | Ubuntu Server 24.04.4 LTS with Apache HTTP Server | Complete |

---

## Virtualized Infrastructure

### Decision

The environment is deployed as a virtualized infrastructure lab.

### Rationale

Virtualization allows several infrastructure systems to run on a single physical host while keeping each role separated.

This supports:

- Repeatable deployment
- Snapshot-based recovery
- Easier testing
- Isolated lab networking
- Lower hardware requirements
- Clear separation between firewall, server, workstation, and web service roles

---

## Central Firewall and Gateway

### Decision

FW-01 was deployed as the central firewall, default gateway, NAT device, DHCP provider, and remote administration entry point.

### Rationale

Using a dedicated firewall keeps the network edge separate from server roles.

FW-01 handles traffic between the internal infrastructure network and upstream connectivity. It also centralizes routing, NAT, firewall rules, DHCP, and Tailscale-based access.

### Current Responsibilities

FW-01 provides:

- Default gateway services
- Network routing
- NAT
- DHCP
- Firewall policy enforcement
- Remote administration through Tailscale

The default gateway for the internal network is:

```text
10.10.10.1
```

The internal network is:

```text
10.10.10.0/24
```

---

## Active Directory Domain Services

### Decision

DC-01 was deployed as the Windows Server Domain Controller for the environment.

### Rationale

Active Directory is required to provide domain-based identity, authentication, DNS integration, and Group Policy management for Windows systems.

DC-01 gives the lab a central Windows administration point and allows WS-01 to be managed as a domain workstation.

### Current Domain Model

| Property | Value |
|----------|-------|
| Domain | primesec.local |
| NetBIOS Name | PRIMESEC |
| Domain Controller | DC-01 |
| Domain Controller IP Address | 10.10.10.10 |
| DNS Model | Active Directory Integrated DNS |

---

## DNS Authority Model

### Decision

DC-01 is the authoritative internal DNS server for the Active Directory domain.

The current AD/domain namespace is:

```text
primesec.local
```

### Rationale

Active Directory relies on DNS for domain controller discovery, authentication, service location, and domain-joined system operation.

For that reason, domain-joined systems should use DC-01 as their DNS server.

### DNS Responsibilities

| Function | Responsible System |
|----------|--------------------|
| Active Directory DNS | DC-01 |
| Internal domain namespace | primesec.local |
| DNS server for domain-joined systems | DC-01 / 10.10.10.10 |
| Gateway and DHCP services | FW-01 |
| Optional upstream/external DNS forwarding for non-domain or network-level services | FW-01 |

Older references to `primesec.internal` are legacy lab naming and are not part of the current DNS model.

---

## DHCP Ownership

### Decision

FW-01 owns DHCP for the internal infrastructure network.

### Rationale

Keeping DHCP on FW-01 keeps the network services split simple:

- FW-01 handles gateway, DHCP, NAT, firewalling, and remote access.
- DC-01 handles Active Directory and internal domain DNS.

This avoids adding Windows DHCP at this stage while still keeping the client configuration aligned with the domain DNS design.

### DHCP Client Configuration

DHCP is configured to provide the following values to clients:

| Setting | Value |
|---------|-------|
| Gateway | 10.10.10.1 |
| DNS Server | 10.10.10.10 |
| Domain/Search Suffix | primesec.local |
| DHCP Scope Range | 10.10.10.100 - 10.10.10.199 |

Validation evidence shows that WS-01 received a dynamic DHCP lease from FW-01.

| Item | Verified Value |
|------|----------------|
| Client Hostname | WS-01 |
| Lease Address | 10.10.10.152 |
| Lease Type | Dynamic |

---

## Windows Workstation Integration

### Decision

WS-01 was deployed as a domain-joined Windows workstation.

### Rationale

A domain controller needs at least one domain-joined client to validate authentication, DNS, Group Policy processing, and workstation management.

WS-01 provides that validation target.

Current WS-01 state:

| Property | Value |
|----------|-------|
| Hostname | WS-01 |
| Operating System | Windows 11 Pro |
| Domain | primesec.local |
| Current DHCP Lease | 10.10.10.152 |
| Lease Type | Dynamic |

---

## Linux Web Server

### Decision

WEB-01 was deployed as a Linux-based Apache web server.

### Rationale

WEB-01 adds a Linux server role to the environment and provides a simple service that can be tested from the internal network.

It is intentionally limited to a basic Apache deployment. The focus is server deployment, service management, firewall configuration, and validation rather than web application development.

Current WEB-01 state:

| Property | Value |
|----------|-------|
| Hostname | WEB-01 |
| Operating System | Ubuntu Server 24.04.4 LTS |
| Primary Service | Apache HTTP Server |
| IP Address | 10.10.10.11 |

---

## Remote Administration

### Decision

Remote administration is provided through Tailscale on FW-01.

### Rationale

Administrative access should not require exposing firewall management services directly to the public Internet.

Tailscale provides a controlled remote access path for administration while keeping the management interface away from direct public exposure.

---

## Group Policy

### Decision

Group Policy was implemented through DC-01 and applied to the domain environment.

### Rationale

Group Policy provides a central way to configure domain and workstation settings.

Implemented policies include:

- GPO-Domain-Password-Policy
- GPO-Interactive-Logon-Notice
- GPO-Workstation-Security-Baseline
- GPO-Workstation-Windows-Update

Exported Group Policy reports are stored under:

```text
reports/gpo/
```

---

## Documentation and Evidence

### Decision

Documentation and validation screenshots are stored in the repository.

### Rationale

The lab should be understandable from the documentation without requiring access to the running virtual machines.

Validation evidence exists for:

- FW-01 connectivity, DNS, DHCP, and Tailscale access
- DC-01 Active Directory, DNS, and domain controller health
- WS-01 domain membership and Group Policy processing
- WEB-01 connectivity, DNS resolution, Apache status, firewall state, service startup, and web page access

---

## Architecture Diagram Status

The existing architecture diagram files are retained:

- `diagrams/architecture.drawio`
- `diagrams/architecture.png`

The diagram still needs to be refreshed to fully reflect the completed DC-01 and WS-01 implementation.

No diagram regeneration was performed during this documentation update.

---

## Design Summary

The current Phase 1 design uses a simple internal network:

- FW-01 handles firewalling, gateway services, NAT, DHCP, and remote administration.
- DC-01 handles Active Directory, authoritative internal DNS, and Group Policy.
- WS-01 validates domain membership, DHCP client configuration, and Group Policy processing.
- WEB-01 provides a basic Linux-hosted Apache service.

The scope is intentionally limited so that each component has a clear role and can be documented and validated.