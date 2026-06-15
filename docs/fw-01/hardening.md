# FW-01 Hardening

## HTTPS Management Interface

### Configuration
- HTTPS enabled for Web GUI access.
- HTTP Strict Transport Security (HSTS) enabled.

### Purpose
Encrypts administrative traffic and prevents browsers from using insecure HTTP connections.

---

## Session Management

### Configuration
- Web GUI session timeout set to 30 minutes.

### Purpose
Reduces the risk of unauthorized access from unattended administrative sessions.

---

## Administrative Accounts

### Configuration
- Dedicated `sysadmin` account created.
- Administrative privileges assigned through the `admins` group.

### Purpose
Avoids the use of shared administrative accounts and improves accountability.

---

## Multi-Factor Authentication (TOTP)

### Configuration
- Local OTP authentication server configured.
- TOTP seed enrolled using Ente Auth.
- OTP authentication successfully validated.

### Purpose
Adds a second authentication factor and reduces the impact of password compromise.

### Notes
- Authentication format: **OTP + Password**
- Example: `123456MySecurePassword!`

---

## Remote Administration

### Configuration
- Tailscale VPN deployed for remote administration.
- FW-01 configured as a subnet router.
- Management access performed through Tailscale.

### Purpose
Eliminates direct exposure of management services to the Internet while providing secure encrypted access.

---

## Firewall Management Restrictions

### Configuration
- `MGMT_TAILSCALE` alias created.
- Administrative access restricted to approved management hosts.

### Purpose
Limits administrative access to trusted devices only.

---

## Logging

### Configuration
- Web GUI access logging enabled.
- Server error logging enabled.

### Purpose
Provides auditability and assists troubleshooting and incident investigation.

---

## Console Protection

### Configuration
- Console menu password protection enabled.

### Purpose
Prevents unauthorized local administrative access.

---

## SSH

### Configuration
- SSH service disabled.

### Purpose
Reduces the attack surface by removing an unnecessary management service.

---

## Firmware Maintenance

### Configuration
- OPNsense upgraded to version 26.1.9.

### Purpose
Ensures security patches, bug fixes and platform improvements are applied.

### Notes

Following the upgrade, the Tailscale integration required manual recovery:

- Reassigned the Tailscale interface.
- Re-enabled the interface assignment.
- Restored subnet advertisement.
- Recreated required firewall rules.
- Validated remote access through Tailscale.

---

## Configuration Backups

### Current State

Configuration backups are performed manually after significant configuration changes.

### Purpose

Provides a recovery mechanism in case of:

- Configuration corruption
- Failed upgrades
- Accidental changes
- Disaster recovery scenarios

### Future Improvement

Implement automated encrypted configuration backups.

---

## Future Improvements

- SSH public key authentication (if SSH is required).
- Suricata IDS deployment.
- CrowdSec integration.
- Automated encrypted configuration backups.
- Additional management access restrictions.