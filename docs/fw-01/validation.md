# FW-01 Validation

## Purpose

This document records the validation procedures performed on FW-01 to verify core networking, DHCP, name resolution, and remote administration functionality.

The objective of these tests is to confirm that FW-01 is operating correctly as the firewall, gateway, NAT device, DHCP owner, and secure remote administration entry point for the PrimeSec Infrastructure environment.

Only completed validation procedures are documented within this file.

---

## Validation Date

June 2026

---

## Internet Connectivity Validation

### Objective

Verify that FW-01 can successfully communicate with external network destinations.

### Procedure

From the OPNsense console, the following command was executed:

```bash
ping -c 4 1.1.1.1
```

The test was used to confirm outbound connectivity from FW-01 to an external IP address.

### Validation Results

The validation completed successfully.

Confirmed results:

- FW-01 reached an external network destination.
- ICMP communication was successful.
- Internet connectivity from the firewall was operational.

This confirms that FW-01 has functional upstream connectivity and can provide external network access for infrastructure systems behind it.

### Evidence

![Internet Connectivity Validation](../../assets/fw-01/ping-validation.png)

---

## DNS Resolution Validation

### Objective

Verify that FW-01 can successfully resolve external domain names using its configured DNS services.

### Procedure

From the OPNsense console, the following command was executed:

```bash
drill google.com
```

The test validated successful DNS query processing and external name resolution from FW-01.

### Validation Results

The validation completed successfully.

Confirmed results:

- DNS query completed successfully.
- A valid DNS response was returned.
- No DNS errors were reported during the validation.

This confirms that FW-01 can perform external DNS lookups required for normal network operations.

### Evidence

![DNS Resolution Validation](../../assets/fw-01/dns-validation.png)

---

## DHCP Validation

### Objective

Verify that FW-01 provides DHCP services for the internal LAN network and that a client system can receive a dynamic lease.

### Validation Results

The validation completed successfully.

Confirmed DHCP information:

| Item                  | Verified Value              |
| --------------------- | --------------------------- |
| DHCP Owner            | FW-01                       |
| Interface             | LAN                         |
| DHCP Scope Range      | 10.10.10.100 - 10.10.10.199 |
| Observed Client Lease | WS-01                       |
| WS-01 Lease Address   | 10.10.10.152                |
| Lease Type            | Dynamic                     |
| Hostname Shown        | WS-01                       |

This confirms that FW-01 is providing DHCP leases on the LAN interface and that WS-01 successfully received a dynamic address from the configured DHCP range.

### Evidence

![DHCP Range Validation](../../assets/fw-01/dhcp-ranges.png)

![DHCP Lease Validation](../../assets/fw-01/dhcp-leases.png)

---

## Remote Administration Validation

### Objective

Verify that FW-01 can be securely administered remotely without exposing management services directly to the public Internet.

### Procedure

The OPNsense Web GUI was accessed through the firewall's assigned Tailscale address from an authorized administrative workstation.

The connection was established through the Tailscale mesh VPN without requiring public port forwarding or direct Internet exposure.

Sensitive addressing information has been partially redacted in the evidence screenshot.

### Validation Results

The validation completed successfully.

Confirmed results:

- OPNsense Web GUI was reachable remotely.
- Login page displayed successfully.
- Administrative access was available through Tailscale.
- No public management exposure was required.

This confirms that remote administration functionality is operational and aligns with the project's secure management design.

### Evidence

![Remote Administration Validation](../../assets/fw-01/tailscale-validation.png)

---

## Validation Summary

| Validation            | Status |
| --------------------- | ------ |
| Internet Connectivity | Passed |
| DNS Resolution        | Passed |
| DHCP                  | Passed |
| Remote Administration | Passed |

---

## DNS Authority Note

FW-01 DNS validation confirms that the firewall can resolve external domain names.

It does not make FW-01 the authoritative DNS server for the Active Directory domain.

The final internal DNS model is:

| Function                       | System                      |
| ------------------------------ | --------------------------- |
| Active Directory DNS authority | DC-01 / 10.10.10.10         |
| Internal AD namespace          | primesec.local              |
| Default gateway                | FW-01 / 10.10.10.1          |
| DHCP ownership                 | FW-01                       |
| DHCP scope range               | 10.10.10.100 - 10.10.10.199 |

FW-01 may provide upstream or external DNS forwarding for non-domain or network-level services, but DC-01 remains authoritative for the `primesec.local` Active Directory domain.

---

## Conclusion

FW-01 successfully passed the completed validation procedures documented in this file.

The results confirm:

- Operational Internet connectivity
- Functional external DNS resolution
- DHCP service operation on the LAN interface
- Successful dynamic lease assignment to WS-01
- Secure remote administration through Tailscale

These validation activities demonstrate that FW-01 is functioning as the foundational networking and security component of the PrimeSec Infrastructure environment.