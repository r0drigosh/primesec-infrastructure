# WEB-01 Overview

## Purpose

`WEB-01` is the internal Ubuntu Server web component for the PrimeSec Infrastructure environment.

It runs Apache HTTP Server and provides a simple internal web endpoint for service, firewall, DNS, and connectivity validation.

---

## Environment Role

`WEB-01` hosts an internal HTTP service behind `FW-01`.

The server is intentionally lightweight. Its role is to provide a predictable Linux-based web service inside the infrastructure network, not to act as a public web application platform.

---

## System Summary

| Property | Value |
| --- | --- |
| Component | `WEB-01` |
| Operating system | Ubuntu Server `24.04.4 LTS` |
| Virtualization platform | Proxmox VE |
| Web service | Apache HTTP Server |
| Role | Internal Linux web server |

---

## Network Summary

| Property | Value |
| --- | --- |
| Internal network | `10.10.10.0/24` |
| Static IP address | `10.10.10.11` |
| Default gateway | `FW-01` / `10.10.10.1` |
| Internal DNS authority | `DC-01` / `10.10.10.10` |
| DNS namespace | `primesec.local` |

`WEB-01` is documented as an internal service on the PrimeSec infrastructure network.

---

## Key Functions

### Apache HTTP Server

`WEB-01` hosts a lightweight Apache landing page for internal service validation.

The documented web endpoint is:

`http://10.10.10.11`

### Static Network Addressing

`WEB-01` uses the static IP address `10.10.10.11`.

This keeps the service reachable through a predictable internal endpoint.

### Host Firewall

`UFW` is enabled on `WEB-01`.

The firewall allows the documented administration and web service ports while denying unsolicited inbound traffic by default.

### Remote Administration

SSH access is allowed on `22/tcp` for server administration.

### Service Startup

Apache and `UFW` are enabled to start automatically with the system.

---

## Related Documentation

| Document | Purpose |
| --- | --- |
| [WEB-01 Hardening](hardening.md) | Operational hardening notes for Apache, `UFW`, SSH exposure, and service startup |
| [WEB-01 Design Decisions](design-decisions.md) | Practical reasoning behind the WEB-01 implementation |
| [WEB-01 Validation](validation.md) | Validation evidence for host identity, service state, firewall policy, DNS resolution, connectivity, and web access |

---

## Validation Reference

`WEB-01` validation is documented in [WEB-01 Validation](validation.md).

Validation covers:

- Host identity
- External network connectivity
- DNS resolution
- Apache service status
- `UFW` firewall policy
- Apache and `UFW` startup state
- Website access at `http://10.10.10.11`
