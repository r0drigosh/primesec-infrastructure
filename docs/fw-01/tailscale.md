# FW-01 Tailscale Integration

## Purpose

Tailscale provides remote administration access to the PrimeSec Infrastructure environment.

`FW-01` acts as the Tailscale entry point for firewall administration and internal subnet access.

---

## Role

`FW-01` uses Tailscale to support remote management without exposing the OPNsense management interface directly to the public Internet.

The firewall also acts as a subnet router for the internal infrastructure network.

---

## Configuration Summary

| Item | Value |
| -------- | -------- |
| Component | `FW-01` |
| Platform | OPNsense |
| Tailscale Interface | `tailscale0` |
| Advertised Subnet | `10.10.10.0/24` |
| Remote Access Path | Tailscale mesh VPN |
| Management Scope | Approved management hosts |

---

## Access Model

Remote administration uses Tailscale as the management path.

```text
Admin workstation
    ↓
Tailscale network
    ↓
FW-01 Tailscale interface
    ↓
OPNsense Web GUI
```

This keeps firewall administration separate from public Internet exposure.

---

## Subnet Routing

`FW-01` advertises the internal infrastructure subnet through Tailscale.

```text
10.10.10.0/24
```

Approved Tailscale clients can reach internal infrastructure systems when route approval and firewall policy allow it.

---

## Firewall Dependencies

Tailscale remote administration depends on:

- Assigned Tailscale interface
- Enabled Tailscale service
- Subnet route advertisement
- Firewall rules allowing approved management traffic
- `MGMT_TAILSCALE` alias for trusted management hosts

---

## Maintenance Checks

After OPNsense firmware maintenance, Tailscale should be revalidated.

Recommended checks:

- Tailscale service state
- Tailscale interface assignment
- Tailscale interface enabled state
- Advertised subnet routes
- Firewall rules for management access
- Web GUI reachability through Tailscale

---

## Validation Reference

Tailscale validation evidence is documented in [FW-01 Validation](validation.md).

The validation shows the OPNsense Web GUI login page reachable through a redacted Tailscale address.