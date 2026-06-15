# WEB-01 Hardening

## System Updates

### Configuration

The operating system was fully updated following deployment using the Ubuntu package management system.

Security updates and package updates were applied to ensure the server was operating with the latest available fixes and security patches.

### Purpose

Maintaining current software versions reduces exposure to known vulnerabilities and improves overall system stability.

Regular patching is a fundamental security practice for Linux server administration and helps minimize the attack surface presented by outdated software.

---

## Host-Based Firewall (UFW)

### Configuration

Uncomplicated Firewall (UFW) was enabled and configured as the host-based firewall for WEB-01.

The firewall service was enabled and configured to start automatically during system boot.

### Evidence

![Firewall Validation](../../assets/web-01/firewall-validation.png)

### Purpose

A host-based firewall provides an additional security layer by controlling network traffic directly at the operating system level.

This reduces unnecessary exposure and ensures that only required services are accessible.

---

## Firewall Policy

### Configuration

The following firewall policy was implemented:

| Policy | Configuration |
|----------|---------------|
| Incoming Traffic | Deny by Default |
| Outgoing Traffic | Allow by Default |

Permitted services:

| Service | Port |
|----------|------|
| SSH | 22/TCP |
| HTTP | 80/TCP |

No additional inbound services were permitted.

### Purpose

A default-deny approach limits exposure by blocking unsolicited inbound connections unless explicitly authorized.

Only services required for administration and web hosting were permitted, reducing the server's attack surface.

---

## SSH Configuration

### Configuration

SSH was enabled to support remote administration.

Administrative access is performed through OpenSSH and restricted to authorized users.

Root SSH login was disabled as part of the server hardening process.

### Purpose

SSH provides secure remote administration capabilities while eliminating the need for direct console access.

Disabling root SSH login reduces the risk associated with privileged account targeting and aligns with common Linux security practices.

---

## Root Account Protection

### Configuration

The local root account was locked.

Direct root SSH authentication was disabled.

Administrative tasks are performed through authorized user accounts with elevated privileges when required.

### Purpose

Restricting direct root access reduces the likelihood of unauthorized privileged access and improves accountability by ensuring administrative actions are performed through individual user accounts.

This approach follows the principle of least privilege and supports secure administrative operations.

---

## Service Minimization

### Configuration

Only services required for the intended role of the server were deployed and enabled.

Active infrastructure services include:

- OpenSSH Server
- Apache HTTP Server
- UFW Firewall

No unnecessary infrastructure services were installed or exposed.

### Purpose

Reducing the number of installed and running services decreases the system attack surface and lowers operational complexity.

Service minimization is a core hardening practice that helps reduce potential entry points for attackers.

---

## Automatic Security Updates

### Configuration

Automatic security updates were enabled using the Ubuntu unattended-upgrades mechanism.

The system is configured to automatically install applicable security updates released through the Ubuntu repositories.

### Purpose

Automatic security updates help ensure that critical security patches are applied in a timely manner and reduce the operational overhead associated with manual patch management.

This improves long-term system security and helps maintain a consistent security baseline.

---

## Security Benefits

The hardening measures implemented on WEB-01 provide several security benefits:

- Reduced attack surface through service minimization
- Protection against unsolicited inbound connections
- Secure remote administration practices
- Elimination of direct root access
- Improved patch management
- Consistent firewall enforcement
- Reduced exposure to known vulnerabilities
- Improved operational security posture

These controls establish a practical baseline security configuration suitable for a Linux server operating within the PrimeSec Infrastructure environment.

---

## Future Improvements

The following enhancements may be considered in future project phases:

- SSH key-based authentication
- Apache hardening controls
- Intrusion detection and monitoring
- Centralized log collection
- HTTPS implementation
- Security auditing and compliance validation
- Vulnerability scanning integration

These items fall outside the scope of the current Phase 1 implementation and are documented as potential future enhancements rather than completed controls.