# WS-01 Overview

## Purpose

WS-01 is the Windows workstation in the PrimeSec Infrastructure environment.

It runs Windows 11 Enterprise and is joined to the `primesec.local` Active Directory domain. The workstation is used to validate domain membership, DHCP client configuration, DNS dependency, user authentication, and Group Policy processing.

---

## Key Responsibilities

WS-01 is used for:

- Domain-based user authentication
- Active Directory integration testing
- Group Policy processing validation
- Workstation configuration validation
- Interactive logon notice validation
- DHCP client validation

---

## System Specifications

| Property | Value |
|----------|-------|
| Hostname | WS-01 |
| Operating System | Windows 11 Enterprise |
| Platform | Proxmox VE |
| Current DHCP Lease Address | 10.10.10.152 |
| Lease Type | Dynamic |
| DHCP Provider | FW-01 |
| Domain Membership | primesec.local |
| Network | 10.10.10.0/24 |
| Role | Domain-Joined Workstation |
| Management Model | Active Directory and Group Policy |

---

## Network Configuration

WS-01 receives its network configuration from FW-01 through DHCP.

Observed DHCP lease:

| Item | Verified Value |
|------|----------------|
| DHCP Provider | FW-01 |
| Client Hostname | WS-01 |
| Lease Address | 10.10.10.152 |
| Lease Type | Dynamic |
| DHCP Scope Range | 10.10.10.100 - 10.10.10.199 |

The address `10.10.10.152` should be treated as the current observed DHCP lease, not as a static workstation address.

---

## Domain Membership

WS-01 was successfully joined to the `primesec.local` Active Directory domain.

Domain membership allows WS-01 to authenticate users through DC-01 and receive domain-based configuration through Group Policy.

The workstation was validated using the domain account **PS User**, confirming that domain authentication and communication with DC-01 were functioning.

### Evidence

![Domain Membership](../../assets/ws-01/domain-membership.png)

---

## Active Directory Integration

WS-01 has a computer account in Active Directory and operates as a domain member.

Through this integration, WS-01 can:

- Authenticate domain users
- Locate domain services through DNS
- Process Group Policy Objects
- Receive workstation configuration from DC-01

This confirms that the domain controller is not only deployed, but also being used by a client system.

---

## Group Policy Integration

Workstation configuration is managed through Active Directory Group Policy.

The applied policies were validated using GPResult.

Applied policies include:

- GPO-Workstation-Security-Baseline
- GPO-Workstation-Windows-Update
- GPO-Interactive-Logon-Notice
- GPO-Domain-Password-Policy
- Default Domain Policy

These policies confirm that WS-01 can receive and process configuration from DC-01.

### Evidence

![Applied Group Policies](../../assets/ws-01/gpresult-validation.png)

---

## Interactive Logon Notice

The interactive logon notice was deployed through Group Policy and validated on WS-01.

This confirms that user-facing policy settings are applied on the workstation.

### Evidence

![Interactive Logon Notice](../../assets/ws-01/interactive-logon-notice.png)

---

## Relationship with DC-01

WS-01 relies on DC-01 for domain services.

DC-01 provides:

- User authentication
- Active Directory services
- DNS resolution for the AD domain
- Group Policy deployment
- Security policy configuration

For domain operation, WS-01 must be able to reach DC-01 and use it as the internal DNS authority.

---

## Relationship with FW-01

WS-01 relies on FW-01 for network access.

FW-01 provides:

- DHCP lease assignment
- Default gateway services
- Routing
- NAT
- Firewalling

The current verified DHCP lease for WS-01 is:

```text
10.10.10.152
```

---

## Operational Role

Within the Phase 1 environment, WS-01 is the client system used to verify that the Windows domain is functioning beyond the domain controller itself.

It provides validation for:

- Domain join
- Domain user authentication
- Group Policy processing
- Interactive logon notice deployment
- DHCP lease assignment
- Client communication with DC-01 and FW-01

---

## Summary

WS-01 is a Windows 11 Enterprise workstation joined to the `primesec.local` domain.

It receives a dynamic DHCP lease from FW-01 and uses DC-01 for Active Directory, DNS, authentication, and Group Policy. Its validation evidence confirms that the workstation is integrated into the current Phase 1 infrastructure.