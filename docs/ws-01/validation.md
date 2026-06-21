# WS-01 Validation

## Purpose

This document records validation evidence for `WS-01`.

Validation covers workstation identity, domain integration, computer Group Policy processing, applied Group Policy Objects, the interactive logon notice, and the documented dynamic DHCP lease.

---

## Validation Summary

| Check | Result |
| --- | --- |
| Workstation identity | Passed |
| Domain integration | Passed |
| Computer Group Policy processing | Passed |
| Applied Group Policy Objects | Passed |
| Interactive logon notice | Passed |
| Dynamic DHCP lease reference | Documented |

---

## Workstation Identity Validation

### Objective

Verify the visible workstation name and domain-style device name for `WS-01`.

### Result

The evidence shows the following workstation identity details:

| Property | Value |
| --- | --- |
| Device name | `WS-01` |
| Full device name | `WS-01.primesec.local` |
| System type | `64-bit operating system, x64-based processor` |

The full device name confirms that the workstation is using the `primesec.local` domain namespace.

### Evidence

![Domain Membership](../../assets/ws-01/domain-membership.png)

---

## Domain and Group Policy Processing Validation

### Objective

Verify that `WS-01` is operating as a domain workstation and can process computer Group Policy from `DC-01`.

### Procedure

```powershell
gpresult /scope computer /r
```

### Result

The `gpresult` output confirms computer-side domain integration and Group Policy processing.

Recorded output includes:

| Property | Value |
| --- | --- |
| Computer | `WS-01` |
| OS configuration | `Member Workstation` |
| Computer account path | `CN=WS-01,OU=Workstations,OU=PRIMESEC,DC=primesec,DC=local` |
| Group Policy source | `DC-01.primesec.local` |
| Domain name | `PRIMESEC` |
| Slow link detected | `No` |

This confirms that `WS-01` can retrieve computer policy from the domain controller and process domain-based workstation configuration.

### Evidence

![Group Policy Result](../../assets/ws-01/gpresult-validation.png)

---

## Applied Group Policy Objects Validation

### Objective

Verify that the expected Group Policy Objects are applied to `WS-01`.

### Result

The `gpresult` output shows the following applied GPOs:

- `GPO-Workstation-Security-Baseline`
- `GPO-Workstation-Windows-Update`
- `GPO-Interactive-Logon-Notice`
- `GPO-Domain-Password-Policy`
- `Default Domain Policy`

This confirms that workstation-level and domain-level policies are being applied to the workstation.

Detailed GPO configuration is documented in [DC-01 Group Policy](../dc-01/group-policy.md).

### Evidence

![Applied Group Policies](../../assets/ws-01/gpresult-validation.png)

---

## Interactive Logon Notice Validation

### Objective

Verify that the interactive logon notice configured through Group Policy appears on `WS-01`.

### Result

The workstation displays the configured logon notice before sign-in.

Visible notice content:

| Field | Value |
| --- | --- |
| Title | `PrimeSec Infrastructure` |
| Message | `Authorized Access Only. This workstation is managed by PrimeSec Infrastructure. Unauthorized use is prohibited and may be monitored.` |

This confirms that the interactive logon notice policy is applied on the workstation.

### Evidence

![Interactive Logon Notice](../../assets/ws-01/interactive-logon-notice.png)

---

## DHCP Lease Reference

### Objective

Record the documented dynamic DHCP lease for `WS-01`.

### Result

`WS-01` is documented with a dynamic DHCP lease from `FW-01`.

| Property | Value |
| --- | --- |
| DHCP provider | `FW-01` |
| DHCP scope | `10.10.10.100 - 10.10.10.199` |
| Observed lease | `10.10.10.152` |
| Lease type | `dynamic` |
| DHCP DNS server | `DC-01` / `10.10.10.10` |

The DHCP lease evidence is maintained in [FW-01 Validation](../fw-01/validation.md#dhcp-validation), because the lease is visible from the firewall DHCP service rather than the WS-01 screenshots.

---

## Conclusion

`WS-01` validation confirms that the workstation is integrated with the `primesec.local` domain, processes computer Group Policy from `DC-01`, receives the expected applied GPOs, and displays the configured interactive logon notice.

The documented DHCP lease places `WS-01` on the internal `10.10.10.0/24` network as a dynamic client of `FW-01`.

Together, these checks support the documented role of `WS-01` as the Windows 11 Pro domain workstation and Group Policy target for the PrimeSec Infrastructure environment.