# Overview

## Purpose

WS-01 is the primary domain-joined workstation within the PrimeSec Infrastructure environment. It serves as a managed endpoint that demonstrates centralized workstation administration through Active Directory Domain Services (AD DS), DNS integration, and Group Policy management.

The workstation was deployed to validate domain-based administration concepts and to demonstrate how enterprise endpoints can be centrally managed, secured, and maintained within a Windows domain environment.

As a domain member, WS-01 receives authentication services, security policies, and administrative controls from DC-01, providing a realistic representation of a managed enterprise workstation.

---

## Key Responsibilities

WS-01 is responsible for:

- Domain-based user authentication
- Active Directory integration
- Group Policy consumption and enforcement
- Centralized workstation management
- Security policy compliance
- Enterprise endpoint validation
- User access testing and verification

---

## System Specifications

| Property | Value |
|----------|---------|
| Hostname | WS-01 |
| Operating System | Windows 11 Enterprise |
| Platform | Proxmox VE |
| Current DHCP Lease Address | 10.10.10.152 |
| Lease Type | Dynamic |
| DHCP Provider | FW-01 |
| Domain Membership | primesec.local |
| Network | 10.10.10.0/24 |
| Role | Domain-Joined Workstation |
| Management Model | Active Directory & Group Policy |

---

## Network Configuration

WS-01 currently receives its network configuration from FW-01 through DHCP.

The observed DHCP lease is:

| Item | Verified Value |
|------|----------------|
| DHCP Provider | FW-01 |
| Client Hostname | WS-01 |
| Lease Address | 10.10.10.152 |
| Lease Type | Dynamic |
| DHCP Scope Range | 10.10.10.100 - 10.10.10.199 |

This address should be treated as the current observed DHCP lease, not as a manually assigned static workstation address.

---

## Domain Membership

WS-01 was successfully joined to the `primesec.local` Active Directory domain and operates as a managed endpoint within the infrastructure.

Domain membership enables centralized authentication and allows users to authenticate using Active Directory credentials rather than locally managed accounts. This administrative model simplifies account management while providing a consistent user experience across domain-managed systems.

By participating in the domain, WS-01 receives directory services, security policies, and configuration management from DC-01, aligning workstation administration with common enterprise practices.

The workstation was validated using the domain account **PS User**, demonstrating successful authentication through Active Directory and confirming proper communication with domain services.

### Evidence

![Domain Membership](../../assets/ws-01/domain-membership.png)

---

## Active Directory Integration

WS-01 is integrated with the Active Directory environment hosted on DC-01.

The workstation maintains a computer account within the directory and participates in centralized identity and access management processes. Through Active Directory integration, the workstation can authenticate domain users, process Group Policy Objects (GPOs), and consume directory-based services.

This integration enables administrators to manage endpoint configuration through centralized infrastructure components rather than individual workstation administration.

The implementation demonstrates fundamental enterprise administration concepts including directory-based authentication, centralized identity management, and managed endpoint deployment.

---

## Group Policy Integration

Workstation configuration is managed through Active Directory Group Policy.

The applied policies were validated using GPResult, confirming successful Group Policy processing and communication with DC-01.

The following policies are applied to WS-01:

- GPO-Workstation-Security-Baseline
- GPO-Workstation-Windows-Update
- GPO-Interactive-Logon-Notice
- GPO-Domain-Password-Policy
- Default Domain Policy

These policies provide centralized configuration management and ensure that workstation settings remain aligned with organizational standards.

Policy-based management reduces administrative overhead while maintaining consistent security and operational controls across managed systems.

### Evidence

![Applied Group Policies](../../assets/ws-01/gpresult-validation.png)

---

## Workstation Administration Model

WS-01 follows a centralized administration model in which configuration and security controls are managed through Active Directory rather than local workstation settings.

This approach provides several operational advantages:

- Consistent configuration management
- Centralized security enforcement
- Simplified workstation administration
- Reduced configuration drift
- Improved scalability

By separating workstation administration from individual device management, the environment reflects the operational model commonly used within enterprise infrastructure teams.

---

## Relationship with DC-01

WS-01 relies on DC-01 for core infrastructure services required for normal domain operation.

Services provided by DC-01 include:

- User authentication
- Active Directory services
- DNS name resolution
- Group Policy deployment
- Security policy enforcement

WS-01 also relies on FW-01 for network access, including default gateway services and DHCP lease assignment.

This relationship establishes DC-01 as the central management platform while positioning WS-01 as a managed endpoint that consumes those services.

The architecture reflects a standard enterprise deployment model where workstations are centrally administered through Active Directory infrastructure.

---

## Operational Role

Within the PrimeSec Infrastructure environment, WS-01 functions as a production-style managed endpoint used to validate directory services, policy deployment, and workstation administration workflows.

The workstation provides a platform for:

- User authentication testing
- Group Policy validation
- Security policy verification
- Endpoint management validation
- Infrastructure integration testing
- DHCP client validation

Its deployment demonstrates how centralized identity and policy services extend from the domain controller to managed client systems.

---

## Security Benefits

Domain membership provides significant security and operational benefits when compared to standalone workstation administration.

Key benefits include:

- Centralized authentication management
- Consistent password policy enforcement
- Standardized workstation configuration
- Controlled security policy deployment
- Reduced risk of configuration drift
- Simplified administrative oversight

By leveraging Active Directory and Group Policy, security controls can be applied consistently across managed endpoints while reducing reliance on manual configuration processes.

This model improves operational consistency and supports scalable workstation administration practices.

---

## Design Summary

WS-01 serves as the primary managed endpoint within the PrimeSec Infrastructure environment and demonstrates the practical application of centralized workstation administration.

Through integration with Active Directory, DNS, DHCP, and Group Policy, the workstation operates as part of a centrally managed domain infrastructure rather than as an independently administered system.

The deployment demonstrates core enterprise administration concepts including domain membership, centralized authentication, policy-based management, endpoint standardization, DHCP client operation, and Active Directory integration.

Together with DC-01 and FW-01, WS-01 establishes a functional Windows domain environment that showcases realistic infrastructure administration practices and provides a foundation for future expansion of the PrimeSec Infrastructure project.