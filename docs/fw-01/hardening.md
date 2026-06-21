# FW-01 Hardening

## Purpose

This document records the security controls applied to `FW-01`.

The focus is management access, authentication, remote administration, service exposure, logging, maintenance, and configuration recovery.

---

## Management Access

The OPNsense Web GUI is configured for HTTPS management access.

Applied controls:

- HTTPS enabled for Web GUI access
- HTTP Strict Transport Security enabled
- Web GUI session timeout set to 30 minutes

These controls protect administrative traffic and reduce the risk of unattended sessions remaining active.

---

## Administrative Accounts and MFA

A dedicated `sysadmin` account is configured for firewall administration.

Administrative permissions are assigned through the `admins` group.

Local OTP authentication is configured for OPNsense administration using a TOTP authenticator application.

OPNsense local OTP authentication uses the OTP value followed by the account password.

```text
OTP + Password
```

This reduces reliance on shared administrative access and adds a second authentication factor for the firewall management interface.

---

## Remote Administration

Tailscale is used for remote administration of `FW-01`.

Current controls:

- Tailscale deployed on OPNsense
- `FW-01` configured as a Tailscale subnet router
- Management access performed through the Tailscale network
- `MGMT_TAILSCALE` alias used for approved management hosts
- Administrative access restricted to trusted management devices

This provides remote access without exposing the OPNsense management interface directly to the public Internet.

---

## Local Access and Services

Console menu password protection is enabled.

SSH is disabled.

These controls reduce local and remote management exposure by limiting unnecessary administrative access paths.

---

## Logging and Maintenance

Management logging is enabled for:

- Web GUI access
- Server errors

Logging supports troubleshooting, auditability, and investigation of firewall management activity.

After firmware maintenance, Tailscale-related settings should be checked before relying on remote access.

Recommended checks:

- Tailscale service state
- Tailscale interface assignment
- Tailscale interface enabled state
- Subnet advertisement
- Firewall rules for management access
- Remote Web GUI reachability through Tailscale

---

## Configuration Backups

Configuration backups are performed manually after significant configuration changes.

Backups provide a recovery path for:

- Configuration corruption
- Failed upgrades
- Accidental changes
- Firewall rebuilds
