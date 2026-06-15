# FW-01 Validation

## Purpose

This document records the validation procedures performed on FW-01 to verify core networking, name resolution and remote administration functionality.

The objective of these tests is to confirm that FW-01 is operating as the primary gateway and management platform for the PrimeSec Infrastructure environment.

Only completed validation procedures are documented within this file.

---

## Validation Date

June 2026

---

## Internet Connectivity Validation

### Objective

Verify that FW-01 can successfully communicate with external networks and reach Internet resources.

### Procedure

From the OPNsense console, the following command was executed:

```bash
ping -c 4 1.1.1.1
```

## DNS Resolution Validation

### Objective

Verify that FW-01 can successfully resolve domain names using configured DNS services.

### Procedure

From the OPNsense console, the following command was executed:

```bash
drill google.com
```

The test validated successful DNS query processing and name resolution.

### Validation Results

- DNS query completed successfully
- A valid A record was returned
- No errors were reported

This confirms that FW-01 can perform DNS lookups and resolve external hostnames required for normal network operations.

### Evidence

![DNS Resolution Validation](../../assets/fw-01/dns-validation.png)

---

## Remote Administration Validation

### Objective

Verify that FW-01 can be securely administered remotely without exposing management services directly to the public Internet.

### Procedure

The OPNsense Web GUI was accessed through the firewall's assigned Tailscale address from an authorized administrative workstation.

The connection was established through the Tailscale mesh VPN without requiring public port forwarding or direct Internet exposure.

Sensitive addressing information has been partially redacted.

### Validation Results

- OPNsense Web GUI reachable remotely
- Login page displayed successfully
- Administrative access available through Tailscale
- No public management exposure required

This confirms that remote administration functionality is operational and aligns with the project's secure management design.

### Evidence

![Remote Administration Validation](../../assets/fw-01/tailscale-validation.png)

---

## Validation Summary

| Validation | Status |
|------------|--------|
| Internet Connectivity | Passed |
| DNS Resolution | Passed |
| Remote Administration | Passed |

---

## Conclusion

FW-01 successfully passed all completed validation procedures.

The results confirm operational Internet connectivity, functional DNS resolution and secure remote administration capabilities, providing the foundational networking services required by the PrimeSec Infrastructure environment.

These validation activities also demonstrate the successful implementation of the networking, security and remote management controls documented throughout the FW-01 documentation set.