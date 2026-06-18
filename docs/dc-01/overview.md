# Overview

## Purpose

DC-01 is the primary Domain Controller for the PrimeSec Infrastructure environment. It provides centralized identity, authentication, authorization, and name resolution services through Active Directory Domain Services (AD DS) and integrated DNS.

The server establishes the foundation for centralized systems administration by enabling domain-based management of users, groups, computers, and Group Policy Objects (GPOs). As the first Windows infrastructure component within the environment, DC-01 serves as the central management platform for domain resources and security policies.

---

## Key Responsibilities

DC-01 is responsible for:

- Centralized user authentication
- Active Directory administration
- DNS name resolution
- Group Policy deployment
- Domain computer management
- Security policy enforcement

---

## Server Specifications

| Property | Value |
|-----------|---------|
| Hostname | DC-01 |
| Operating System | Windows Server 2022 |
| Platform | Proxmox VE |
| IP Address | 10.10.10.10 |
| Domain Name | primesec.local |
| NetBIOS Name | PRIMESEC |
| DNS Configuration | Active Directory Integrated DNS |
| Server Role | Domain Controller |

---

## Installed Roles and Services

### Active Directory Domain Services (AD DS)

Active Directory Domain Services provides centralized identity and access management for the PrimeSec environment.

Implemented capabilities include:

- Domain authentication
- User and group administration
- Organizational Unit (OU) management
- Group Policy administration
- Computer account management
- Security policy enforcement

The deployment enables centralized administration of Windows-based systems and establishes a scalable directory structure for future infrastructure growth.

---

### DNS

An Active Directory-integrated DNS service was deployed alongside AD DS.

DNS responsibilities include:

- Internal name resolution
- Domain controller service location
- Active Directory service discovery
- Dynamic DNS record registration
- Forward and reverse lookup zone management

The DNS service enables domain-joined systems to locate authentication services, directory resources, and domain controllers required for normal domain operations.

### Evidence

![DNS Forward Lookup Zone](../../assets/dc-01/dns-forward-lookup-zone.png)

---

## Active Directory Design

### Domain Structure

A single-forest, single-domain Active Directory environment was deployed using the following configuration.

| Property | Value |
|-----------|---------|
| Forest Root Domain | primesec.local |
| Domain Type | Single Forest, Single Domain |
| NetBIOS Name | PRIMESEC |

This design reflects a realistic small-to-medium business environment while maintaining simplicity, manageability, and clear administrative boundaries.

### Evidence

![Active Directory Domain Information](../../assets/dc-01/get-addomain.png)

---

### Organizational Unit Hierarchy

The Active Directory structure was designed to logically separate administrative accounts, users, groups, servers, and workstations.

```text
PRIMESEC
├── Admin
├── Groups
├── Servers
├── Users
└── Workstations
```

This hierarchy supports:

- Targeted Group Policy deployment
- Logical object organization
- Simplified administration
- Future infrastructure expansion

### Evidence

![Active Directory OU Structure](../../assets/dc-01/ad-ou-structure.png)

---

### Administrative Separation

Administrative and standard user accounts are separated through dedicated Organizational Units.

This approach provides:

- Clear administrative boundaries
- Simplified privilege management
- More precise policy targeting
- Improved operational consistency

The design aligns with common enterprise administration practices and provides a foundation for future role-based access control implementations.

---

### Scalability Considerations

The directory structure was intentionally designed to support future infrastructure growth without requiring significant redesign.

Potential future expansion includes:

- Additional member servers
- Additional domain workstations
- Department-based Organizational Units
- Additional security groups
- Expanded Group Policy deployment
- File services and shared resources

The current hierarchy provides a scalable foundation while remaining appropriate for a small infrastructure environment.

---

## Design Summary

The deployment of DC-01 establishes the central identity and management platform for the PrimeSec Infrastructure environment.

By combining Active Directory Domain Services, integrated DNS, Organizational Unit design, and centralized policy management, the environment provides a scalable foundation for workstation administration, security enforcement, and future infrastructure expansion.

The implementation demonstrates practical enterprise infrastructure concepts including identity management, directory services, DNS integration, Group Policy administration, security baseline enforcement, and centralized Windows administration.