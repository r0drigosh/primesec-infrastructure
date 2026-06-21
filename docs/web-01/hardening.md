# WEB-01 Hardening

## Purpose

This document records the implemented hardening controls for `WEB-01`.

The scope is limited to the current Ubuntu Server, Apache HTTP Server, `UFW`, SSH exposure, and service startup configuration.

---

## Hardening Summary

| Area | Implemented State |
| --- | --- |
| Host firewall | `UFW` active |
| Default incoming policy | Deny |
| Default outgoing policy | Allow |
| SSH access | Allowed on `22/tcp` |
| HTTP access | Allowed on `80/tcp` |
| Apache service | Active/running |
| Apache startup | Enabled |
| `UFW` startup | Enabled |

---

## Apache HTTP Server

Apache HTTP Server runs on `WEB-01` and serves the internal web page at:

`http://10.10.10.11`

Validated Apache state:

- Service loaded successfully
- Service active/running
- Service enabled at startup
- Web page reachable from the internal environment

Apache is used only for the internal HTTP service documented in this repository.

---

## Host Firewall

`WEB-01` uses `UFW` as its host-based firewall.

The validated firewall policy is:

| Firewall Setting | Value |
| --- | --- |
| Status | Active |
| Logging | On, low |
| Default incoming policy | Deny |
| Default outgoing policy | Allow |
| Default routed policy | Disabled |
| New profiles | Skip |

Allowed inbound services:

| Service | Port |
| --- | --- |
| OpenSSH | `22/tcp` |
| HTTP | `80/tcp` |

The firewall evidence also shows IPv6 allow rules for `22/tcp` and `80/tcp`.

---

## SSH Exposure

SSH is allowed through `UFW` for administrative access to `WEB-01`.

The documented exposed administration port is:

`22/tcp`

No additional remote administration services are documented for this component.

---

## Service Startup

Apache and `UFW` are enabled to start automatically with the system.

Validated startup checks:

- `systemctl is-enabled apache2`
- `systemctl is-enabled ufw`

Both services returned `enabled` in the available evidence.

---

## Network Placement

`WEB-01` is placed on the internal infrastructure network.

| Setting | Value |
| --- | --- |
| Internal IP address | `10.10.10.11` |
| Internal network | `10.10.10.0/24` |
| Default gateway | `FW-01` / `10.10.10.1` |
| Internal DNS authority | `DC-01` / `10.10.10.10` |
| DNS namespace | `primesec.local` |

This keeps the web service reachable as a predictable internal endpoint.

---

## Evidence Reference

Validation evidence is documented in [WEB-01 Validation](validation.md).

The evidence covers:

- Host identity
- Apache service status
- Apache and `UFW` startup state
- `UFW` firewall policy
- External connectivity
- DNS resolution
- Web page access