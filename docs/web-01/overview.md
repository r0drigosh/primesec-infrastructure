# WEB-01 Overview

## Purpose

`WEB-01` is the internal Linux web server for the PrimeSec Infrastructure environment.

It runs Ubuntu Server 24.04.4 LTS and Apache HTTP Server, using a static IP address on the internal network.

---

## Environment Role

`WEB-01` provides a simple internal HTTP service behind `FW-01`.

The server supports internal web access, static addressing, service availability checks, host-based firewall policy, and DNS validation from the infrastructure network.

---

## System Summary

| Property | Value |
| -------- | -------- |
| Component | `WEB-01` |
| Operating System | Ubuntu Server 24.04.4 LTS |
| Virtualization Platform | Proxmox VE |
| Role | Internal Linux web server |

---

## Network Summary

| Property | Value |
| -------- | -------- |
| Network | `10.10.10.0/24` |
| Static IP Address | `10.10.10.11` |
| Default Gateway | `FW-01` / `10.10.10.1` |
| Internal DNS Authority | `DC-01` / `10.10.10.10` |

`WEB-01` is published internally through Apache HTTP Server and protected locally with UFW.

---

## Key Functions

### Apache HTTP Server

`WEB-01` hosts a lightweight Apache landing page for internal service validation.

The HTTP service is used to confirm that the server can deliver web content across the internal network.

### Static Network Configuration

`WEB-01` uses the static IP address `10.10.10.11`.

This keeps the web service reachable through a predictable internal endpoint.

### Host-Based Firewall

UFW is enabled on `WEB-01`.

The documented firewall policy permits required administration and web traffic while denying unsolicited inbound traffic by default.

### Remote Administration

SSH is enabled for remote administration of the Linux server.

### System Maintenance

Automatic security updates are enabled using the Ubuntu unattended-upgrades mechanism.

---

## Related Documentation

| Document | Purpose |
| -------- | -------- |
| [WEB-01 Deployment](web-01.md) | Deployment and configuration state |
| [WEB-01 Hardening](hardening.md) | Linux hardening controls applied to WEB-01 |
| [WEB-01 Design Decisions](design-decisions.md) | Design rationale for the WEB-01 implementation |
| [DNS Configuration](../networking/dns.md) | DNS model used by the infrastructure |
| [WEB-01 Validation](validation.md) | Validation evidence for network, service, firewall, and web access checks |

---

## Validation Reference

`WEB-01` validation is documented in [WEB-01 Validation](validation.md).

Validation covers:

- Network connectivity through `FW-01`
- DNS resolution
- Apache service status
- UFW firewall configuration
- Service startup configuration
- Website access from the internal network