# WEB-01 Design Decisions

## Purpose

This document explains the practical design choices behind `WEB-01`.

`WEB-01` is the internal Ubuntu Server and Apache HTTP Server component in the PrimeSec Infrastructure environment.

---

## Design Summary

| Area | Decision |
| --- | --- |
| Server operating system | Ubuntu Server `24.04.4 LTS` |
| Web service | Apache HTTP Server |
| Network placement | Internal infrastructure network |
| IP assignment | Static internal IP address |
| Host firewall | `UFW` |
| Web exposure | Internal HTTP on `80/tcp` |
| Administration access | SSH on `22/tcp` |

---

## Ubuntu Server

Ubuntu Server `24.04.4 LTS` provides a stable Linux server base for the internal web component.

It is suitable for this role because it provides:

- Standard Linux server administration
- Predictable package and service management
- Straightforward Apache deployment
- Long-term maintenance through an LTS release

---

## Apache HTTP Server

Apache HTTP Server is used to host the internal web page for `WEB-01`.

Apache fits this project because it is:

- Simple to deploy on Ubuntu Server
- Easy to manage through `systemd`
- Easy to validate through service status checks and browser access
- Appropriate for a lightweight internal HTTP endpoint

In this environment, Apache provides a clear service target for web access, firewall validation, and network connectivity checks.

---

## Static Internal IP Address

`WEB-01` uses the static internal IP address:

`10.10.10.11`

A static address keeps the web service predictable for:

- Direct browser access
- Internal DNS mapping
- Firewall validation
- Troubleshooting
- Documentation

---

## Internal Network Placement

`WEB-01` is placed on the internal infrastructure network behind `FW-01`.

| Setting | Value |
| --- | --- |
| Internal network | `10.10.10.0/24` |
| WEB-01 address | `10.10.10.11` |
| Default gateway | `FW-01` / `10.10.10.1` |
| Internal DNS authority | `DC-01` / `10.10.10.10` |
| DNS namespace | `primesec.local` |

This keeps the web server aligned with the internal infrastructure model used by the rest of the lab.

---

## Host Firewall

`UFW` is used as the local host firewall on `WEB-01`.

The documented inbound access is limited to:

| Port | Purpose |
| --- | --- |
| `22/tcp` | SSH administration |
| `80/tcp` | Internal HTTP access |

The default incoming policy denies unsolicited inbound traffic, while the default outgoing policy allows outbound traffic.

---

## Internal HTTP Service

`WEB-01` exposes Apache over `80/tcp` for internal access.

The documented service endpoint is:

`http://10.10.10.11`

This provides a direct validation point for:

- Apache service availability
- Host firewall rules
- Browser-based access
- Internal network reachability

---

## DNS Handling

`DC-01` remains the internal DNS authority for the `primesec.local` namespace.

`WEB-01` documentation references DNS only where it supports service reachability and validation.

The available WEB-01 DNS evidence confirms external DNS resolution from the host. It does not prove direct queries to `DC-01`, because the screenshot shows the local system resolver stub `127.0.0.53`.

---

## Design Boundary

`WEB-01` is documented as a single-purpose internal web server.

The implemented scope includes:

- Ubuntu Server
- Apache HTTP Server
- Static internal addressing
- `UFW` host firewall policy
- SSH administration exposure on `22/tcp`
- Internal HTTP access on `80/tcp`
- Validation evidence under `assets/web-01/`

The component scope is limited to an internal HTTP endpoint with host firewall validation, Apache service validation, and supporting network/DNS checks.
