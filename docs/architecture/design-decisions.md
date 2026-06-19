# Architecture Design Decisions

## Purpose

This document records the main architecture decisions used in the PrimeSec Infrastructure environment.

The goal is to explain why the environment was built in its current form and to provide technical context for instructors, recruiters, and junior Systems Administration reviewers.

This is a junior/internship infrastructure portfolio project. The design intentionally focuses on clarity, practical implementation, and realistic small-environment administration rather than production-scale enterprise complexity.

---

## Current Architecture Scope

The current Phase 1 environment includes the following systems:

| System | Role | Status |
|--------|------|--------|
| FW-01 | Firewall, gateway, NAT, DHCP, remote access entry point | Complete |
| DC-01 | Windows Server Domain Controller, Active Directory, DNS, Group Policy | Complete |
| WS-01 | Windows domain-joined workstation | Complete |
| WEB-01 | Ubuntu Server with Apache HTTP Server | Complete |

---

## Virtualized Infrastructure

### Decision

The environment is deployed as a virtualized infrastructure lab.

### Rationale

Virtualization provides a practical way to build and manage multiple infrastructure systems without requiring separate physical hardware for each server or workstation.

This approach supports:

- Repeatable deployment
- Easier testing
- Snapshot-based recovery
- Isolated infrastructure experimentation
- Cost-effective learning
- Clear portfolio documentation

### Skills Demonstrated

- Virtual machine deployment
- Virtual networking
- Infrastructure segmentation
- System lifecycle management
- Lab environment planning

---

## Central Firewall and Gateway

### Decision

FW-01 was deployed as the central firewall, default gateway, NAT device, DHCP provider, and secure remote access entry point.

### Rationale

Using a dedicated firewall reflects common small-business and lab infrastructure design.

FW-01 provides the network boundary between the internal infrastructure network and upstream connectivity. It also centralizes routing, NAT, firewall policy, and remote administration access.

### Current Responsibilities

FW-01 provides:

- Default gateway services
- Network routing
- NAT
- DHCP
- Firewall policy enforcement
- Secure remote access through Tailscale

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

Active Directory is a core technology for Windows infrastructure administration. Deploying DC-01 allows the project to demonstrate centralized identity, authentication, directory structure, Group Policy, DNS integration, and workstation management.

### Current Domain Model

| Property | Value |
|----------|-------|
| Domain | primesec.local |
| NetBIOS Name | PRIMESEC |
| Domain Controller | DC-01 |
| Domain Controller IP Address | 10.10.10.10 |
| DNS Model | Active Directory Integrated DNS |

### Skills Demonstrated

- Active Directory Domain Services deployment
- Domain design
- User and group administration
- Organizational Unit planning
- Group Policy management
- Centralized Windows administration

---

## DNS Authority Model

### Decision

DC-01 is the authoritative internal DNS server for the Active Directory domain.

The final internal AD/domain namespace is:

```text
primesec.local
```

### Rationale

Active Directory depends heavily on DNS for service discovery, authentication, domain controller location, and domain-joined system operation.

Using DC-01 as the authoritative internal DNS server aligns the DNS design with the Active Directory architecture.

### Final DNS Responsibilities

| Function | Responsible System |
|----------|--------------------|
| Active Directory DNS | DC-01 |
| Internal domain namespace | primesec.local |
| DNS server for domain-joined systems | DC-01 / 10.10.10.10 |
| Gateway and DHCP services | FW-01 |
| Optional upstream/external DNS forwarding for non-domain or network-level services | FW-01 |

Older references to `primesec.internal` are considered legacy lab naming and are not part of the current final DNS model.

---

## DHCP Ownership

### Decision

FW-01 owns DHCP for the internal infrastructure network.

### Rationale

Keeping DHCP on the firewall simplifies the lab design and matches a common small-environment model where the firewall provides basic network services while the Domain Controller provides identity and internal DNS.

This avoids unnecessary Windows DHCP complexity at this stage while still demonstrating a realistic division of responsibilities.

### DHCP Client Configuration

DHCP should provide the following values to clients:

| Setting | Value |
|---------|-------|
| Gateway | 10.10.10.1 |
| DNS Server | 10.10.10.10 |
| Domain/Search Suffix | primesec.local |
| DHCP Scope Range | 10.10.10.100 - 10.10.10.199 |

The exact DHCP scope range is not documented in the current repository sources and should not be invented.

---

## Windows Workstation Integration

### Decision

WS-01 was deployed as a domain-joined Windows workstation.

### Rationale

A domain controller without a managed endpoint does not fully demonstrate centralized administration. WS-01 provides a practical validation target for domain membership, authentication, Group Policy processing, and workstation security controls.

### Skills Demonstrated

- Domain join process
- Workstation identity management
- Group Policy application
- Centralized endpoint administration
- User-facing security policy validation

---

## Linux Web Server

### Decision

WEB-01 was deployed as a Linux-based Apache web server.

### Rationale

A Linux web server adds a non-Windows infrastructure component and demonstrates broader Systems Administration capability.

WEB-01 provides a practical service endpoint for validating:

- Linux server deployment
- Apache service management
- Static server configuration
- Host-based firewall rules
- Network connectivity
- Web service availability

### Scope Control

WEB-01 is intentionally simple. It hosts a lightweight Apache landing page rather than a complex application.

This keeps the project focused on infrastructure administration instead of web development.

---

## Remote Administration

### Decision

Secure remote administration is provided through Tailscale on FW-01.

### Rationale

Remote administration is useful in infrastructure environments, but exposing management interfaces directly to the public Internet would be poor practice.

Using Tailscale allows management access through an encrypted mesh VPN model while keeping administrative services away from direct public exposure.

### Skills Demonstrated

- VPN-based administration
- Secure management access
- Firewall access control
- Remote troubleshooting
- Operational security awareness

---

## Documentation and Evidence

### Decision

Documentation and validation evidence are treated as core project deliverables.

### Rationale

Infrastructure work is not complete unless it can be understood, reviewed, maintained, and validated.

The repository includes technical documentation and screenshots to show that the environment was implemented and tested.

### Evidence Areas

Validation evidence exists for:

- FW-01 connectivity, DNS, and remote administration
- DC-01 Active Directory, DNS, and Domain Controller health
- WS-01 domain membership and Group Policy processing
- WEB-01 connectivity, DNS, Apache, firewall, service startup, and web page access

---

## Architecture Diagram Status

The existing architecture diagram files are retained temporarily:

- `diagrams/v1-architecture.drawio`
- `diagrams/v1-architecture.png`

The diagram is pending update to fully reflect the completed DC-01 and WS-01 implementation.

No diagram regeneration was performed during this documentation correction pass.

---

## Design Summary

PrimeSec Infrastructure uses a simple and realistic small-environment architecture:

- FW-01 provides routing, NAT, DHCP, firewalling, and remote access.
- DC-01 provides Active Directory, authoritative internal DNS, and Group Policy.
- WS-01 demonstrates centralized workstation administration.
- WEB-01 demonstrates Linux server and Apache service administration.

This design is appropriate for a junior/internship infrastructure portfolio because it demonstrates practical systems administration skills without unnecessary enterprise overengineering.