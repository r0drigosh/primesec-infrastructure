# WEB-01 Deployment

## Purpose

This document describes the deployment and configuration state of WEB-01 at a high level.

WEB-01 is the Ubuntu Server component of the PrimeSec Infrastructure environment. It provides a lightweight Apache HTTP service used to demonstrate Linux server administration, service deployment, network configuration, host-based firewalling, and validation practices.

This document does not duplicate `hardening.md`. Security-specific controls are documented separately in the WEB-01 hardening document.

---

## Deployment Scope

WEB-01 was deployed as a dedicated Linux server within the PrimeSec Infrastructure lab.

The deployment focuses on:

- Ubuntu Server administration
- Apache HTTP Server deployment
- Static server networking
- SSH-based administration
- Host-based firewall configuration
- Service startup validation
- Web service availability testing
- Infrastructure documentation

The server is intentionally simple and does not host a complex web application. Its purpose is to demonstrate infrastructure deployment and service management rather than web development.

---

## Verified System State

| Property | Value |
|----------|-------|
| Hostname | web-01 |
| Operating System | Ubuntu Server 24.04.4 LTS |
| Platform Type | Virtual Machine |
| Virtualization Platform | Proxmox VE |
| Primary Service | Apache HTTP Server |
| Network Configuration | Static IP Address |
| Static IP Address | 10.10.10.11 |
| Default Gateway | FW-01 / 10.10.10.1 |
| Internal AD DNS Authority | DC-01 / 10.10.10.10 |
| Internal Domain Namespace | primesec.local |
| Host-Based Firewall | UFW |
| Remote Administration | SSH |
| Automatic Security Updates | Enabled |

---

## Deployment Model

WEB-01 is deployed behind FW-01 on the internal PrimeSec Infrastructure network.

The internal network is `10.10.10.0/24`.

FW-01 provides the default gateway for the environment: `10.10.10.1`.

DC-01 provides authoritative internal DNS for the Active Directory domain: `10.10.10.10`.

The final internal domain namespace is `primesec.local`.

WEB-01 uses the static IP address `10.10.10.11`.

---

## Network Configuration

WEB-01 was configured with static network addressing.

The purpose of using a static address is to ensure that the server remains reachable through a predictable endpoint for administration, validation, and web service access.

Verified network-related characteristics:

- WEB-01 is connected to the internal infrastructure network.
- WEB-01 uses the static IP address `10.10.10.11`.
- WEB-01 uses FW-01 / `10.10.10.1` as the network gateway.
- WEB-01 operates within the final internal DNS model where DC-01 / `10.10.10.10` is the internal AD DNS authority.
- WEB-01 can reach external network destinations.
- WEB-01 can perform DNS resolution.
- WEB-01 can serve HTTP content to clients on the network.

---

## DNS Configuration

The final PrimeSec Infrastructure DNS model uses DC-01 as the authoritative internal DNS server for the Active Directory domain.

| Function | System |
|----------|--------|
| Internal AD DNS authority | DC-01 / 10.10.10.10 |
| Internal namespace | primesec.local |
| Default gateway | FW-01 / 10.10.10.1 |
| DHCP owner | FW-01 |
| WEB-01 static IP address | 10.10.10.11 |

Earlier references to FW-01 as the primary DNS server for internal systems belong to the previous lab naming/design stage and should not be treated as the final Active Directory DNS model.

For internal `primesec.local` resolution, the final design uses DC-01 as the internal DNS authority.

---

## Apache HTTP Server

Apache HTTP Server was installed and configured as the primary service on WEB-01.

The Apache service provides:

- A lightweight internal web page
- A service endpoint for infrastructure validation
- A practical demonstration of Linux service deployment
- A simple target for network and firewall testing

The hosted landing page was validated successfully from the network.

### Evidence

![Website Access Validation](../../assets/web-01/web-page-validation.png)

---

## Service Management

WEB-01 uses systemd service management for infrastructure services.

Validated services include:

- Apache HTTP Server
- UFW firewall

The repository includes validation evidence confirming that required services are enabled for startup.

### Evidence

![Service Startup Validation](../../assets/web-01/service-startup-validation.png)

---

## Host-Based Firewall

UFW is used as the host-based firewall on WEB-01.

The firewall configuration is documented in detail in `docs/web-01/hardening.md`.

The validated firewall posture includes:

- UFW enabled
- Default incoming traffic denied
- Default outgoing traffic allowed
- SSH permitted
- HTTP permitted

### Evidence

![Firewall Validation](../../assets/web-01/firewall-validation.png)

---

## Remote Administration

SSH is enabled for remote administration of WEB-01.

SSH provides command-line access for server management, troubleshooting, package maintenance, service checks, and configuration review.

Security-specific SSH hardening details are documented in `docs/web-01/hardening.md`.

---

## Validation Evidence

WEB-01 validation evidence exists for the following areas:

| Validation Area | Evidence |
|-----------------|----------|
| Network connectivity | `assets/web-01/ping-validation.png` |
| DNS resolution | `assets/web-01/dns-validation.png` |
| Apache service status | `assets/web-01/apache-status-validation.png` |
| Firewall configuration | `assets/web-01/firewall-validation.png` |
| Service startup | `assets/web-01/service-startup-validation.png` |
| Web page access | `assets/web-01/web-page-validation.png` |
| Hostname validation | `assets/web-01/hostname-validation.png` |

Detailed validation results are documented in `docs/web-01/validation.md`.

---

## Relationship with Other Components

### FW-01

WEB-01 relies on FW-01 for:

- Default gateway services
- Routing
- NAT
- External network access
- Network security controls

### DC-01

DC-01 provides the authoritative internal DNS service for the `primesec.local` Active Directory domain.

If WEB-01 needs to resolve internal AD/domain records, DC-01 is the authoritative DNS source.

### Proxmox VE

Proxmox VE provides the virtual machine platform, virtual networking, and lifecycle management for WEB-01.

---

## Deployment Summary

WEB-01 is a completed Linux web server deployment within the PrimeSec Infrastructure environment.

It demonstrates:

- Ubuntu Server deployment
- Apache HTTP Server configuration
- Static network configuration using `10.10.10.11`
- SSH administration
- UFW firewall usage
- Service startup management
- Network and DNS validation
- Web service availability testing
- Professional infrastructure documentation

The deployment is intentionally focused and appropriate for a junior/internship infrastructure portfolio project.