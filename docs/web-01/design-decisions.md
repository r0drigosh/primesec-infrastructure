# WEB-01 Design Decisions

## Purpose

This document records the key architectural and implementation decisions made during the deployment of WEB-01.

The objective is to document the reasoning behind each decision, demonstrate infrastructure planning considerations and provide context for technical reviewers evaluating the PrimeSec Infrastructure project.

---

## Ubuntu Server 24.04.4 LTS Selection

### Decision

Ubuntu Server 24.04.4 LTS was selected as the operating system for WEB-01.

### Rationale

Ubuntu Server is one of the most widely deployed Linux distributions in enterprise, cloud and SMB environments. The Long-Term Support (LTS) release provides stability, extended support and predictable maintenance cycles.

The platform also offers extensive documentation and a large support ecosystem, making it well suited for infrastructure workloads.

### Benefits

- Industry-recognized Linux platform
- Long-Term Support release
- Extensive documentation and community support
- Commonly encountered in Systems Administration roles
- Stable operating environment for hosted services
- Strong package management ecosystem

---

## Apache HTTP Server Selection

### Decision

Apache HTTP Server was selected as the web service platform hosted on WEB-01.

### Rationale

Apache remains one of the most widely used web servers and provides a straightforward platform for demonstrating Linux service deployment and administration.

For the objectives of Phase 1, Apache provides all required functionality without introducing unnecessary complexity.

### Benefits

- Mature and widely adopted web server
- Simple deployment and management
- Extensive documentation
- Demonstrates service installation and administration skills
- Suitable for infrastructure validation and testing

---

## Static IP Address Configuration

### Decision

WEB-01 was configured with a static IPv4 address.

### Rationale

Infrastructure services require predictable network addressing to simplify administration, documentation and troubleshooting.

Using a static address ensures the server remains reachable through a consistent endpoint and avoids dependency on dynamic address assignment.

### Benefits

- Consistent service accessibility
- Simplified troubleshooting
- Improved infrastructure documentation
- Predictable network management
- Aligns with common server deployment practices

---

## SSH Remote Administration

### Decision

SSH was enabled as the primary method of remote administration.

### Rationale

Remote administration is a fundamental requirement for Linux server management.

SSH provides secure command-line access and reflects standard operational practices used within infrastructure and systems administration environments.

### Benefits

- Secure remote administration
- Reduced dependence on direct console access
- Supports troubleshooting and maintenance activities
- Industry-standard management protocol
- Demonstrates Linux administration competency

---

## UFW Firewall Implementation

### Decision

UFW was deployed as the host-based firewall solution for WEB-01.

### Rationale

A host-based firewall provides an additional security layer independent of network perimeter controls.

UFW offers a straightforward management interface while still enforcing effective access control policies.

### Benefits

- Additional security layer
- Reduced attack surface
- Simple rule management
- Clear firewall policy visibility
- Demonstrates Linux security administration skills

---

## Automatic Security Updates

### Decision

Automatic security updates were enabled using Ubuntu's unattended-upgrades mechanism.

### Rationale

Maintaining current security patches is a fundamental operational requirement for server infrastructure.

Automating security updates reduces administrative overhead and improves consistency in patch management.

### Benefits

- Reduced exposure to known vulnerabilities
- Improved patch management
- Lower maintenance requirements
- Consistent security baseline
- Demonstrates security-conscious administration practices

---

## Minimal Landing Page Deployment

### Decision

A lightweight custom landing page was deployed instead of a feature-rich web application.

### Rationale

The purpose of WEB-01 is to demonstrate infrastructure deployment, Linux administration and web service management rather than web development.

A simple landing page provides sufficient validation that the Apache service is operational while keeping the focus on infrastructure skills.

### Benefits

- Supports infrastructure validation
- Keeps project scope focused
- Avoids unnecessary complexity
- Clearly identifies the server role
- Demonstrates successful service deployment

---

## Deployment Behind FW-01

### Decision

WEB-01 was deployed behind FW-01 and uses the firewall as its default gateway.

### Rationale

FW-01 serves as the central routing and security component within the PrimeSec Infrastructure environment.

Placing WEB-01 behind the firewall reflects common infrastructure design principles and centralizes network control.

### Benefits

- Centralized network management
- Consistent routing configuration
- Improved security posture
- Simplified DNS and gateway management
- Demonstrates layered infrastructure design

---

## Documentation-First Approach

### Decision

Documentation was treated as a core project deliverable alongside technical implementation.

### Rationale

Infrastructure environments depend on accurate documentation for administration, troubleshooting and operational continuity.

The project was designed to demonstrate not only technical implementation skills but also the ability to document systems professionally.

### Benefits

- Improves project maintainability
- Demonstrates professional practices
- Enhances recruiter readability
- Supports operational consistency
- Reflects real-world infrastructure workflows

---

## Architectural Summary

The architectural decisions implemented for WEB-01 prioritize simplicity, stability, maintainability and operational realism.

Rather than introducing unnecessary technologies, the deployment focuses on demonstrating core Systems Administration competencies through a properly configured Linux server, a managed web service, host-based security controls, remote administration capabilities and comprehensive documentation.

Collectively, these decisions support the objectives of PrimeSec Infrastructure Phase 1 by showcasing practical infrastructure deployment, Linux administration, service management, security hardening and operational documentation skills expected of junior Systems Administration and Infrastructure candidates.