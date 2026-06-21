# DC-01 Validation

## Purpose

This document records validation evidence for `DC-01`.

Validation covers Active Directory Domain Services, Active Directory Integrated DNS, domain controller health, Organizational Unit structure, and Group Policy configuration.

---

## Validation Summary

| Check | Result |
| --- | --- |
| Active Directory domain configuration | Passed |
| Organizational Unit structure | Passed |
| Active Directory DNS zone | Passed |
| Domain controller health check | Passed |
| Group Policy linking | Passed |
| Implemented GPO settings | Passed |

---

## Domain Configuration Validation

### Objective

Verify that the Active Directory domain is configured with the expected domain name, NetBIOS name, and domain controller identity.

### Procedure

```powershell
Get-ADDomain
```

### Result

The PowerShell output confirms the following domain configuration:

| Property | Value |
| --- | --- |
| Domain | `primesec.local` |
| NetBIOS name | `PRIMESEC` |
| DNS root | `primesec.local` |
| Domain mode | `Windows2016Domain` |
| Domain controller | `DC-01.primesec.local` |

The captured output shows `DC-01.primesec.local` as the domain controller for visible domain role fields.

### Evidence

![Active Directory Domain Information](../../assets/dc-01/get-addomain.png)

---

## Organizational Unit Validation

### Objective

Verify that the expected Organizational Unit structure exists in Active Directory.

### Result

The `PRIMESEC` OU contains the expected administrative structure:

```text
PRIMESEC
├── Admin
├── Groups
├── Servers
├── Users
└── Workstations
```

The evidence also shows example objects placed under the structure, including:

- `PS Admin`
- `GG_Admins`
- `GG_Users`
- `PS User`
- `WS-01`

This confirms that user, group, server, and workstation objects can be separated logically for administration and policy targeting.

### Evidence

![Active Directory OU Structure](../../assets/dc-01/ad-ou-structure.png)

---

## DNS Zone Validation

### Objective

Verify that `DC-01` hosts the Active Directory DNS zone for `primesec.local`.

### Result

DNS Manager shows the `primesec.local` forward lookup zone on `DC-01`.

The zone contains Active Directory DNS folders and host records for core systems.

| Record | Type | Value |
| --- | --- | --- |
| `(same as parent folder)` | `Host (A)` | `10.10.10.10` |
| `dc-01` | `Host (A)` | `10.10.10.10` |
| `fw-01` | `Host (A)` | `10.10.10.1` |
| `WS-01` | `Host (A)` | `10.10.10.152` |

The evidence confirms that `DC-01` is hosting the internal Active Directory DNS namespace for `primesec.local`.

### Evidence

![DNS Forward Lookup Zone](../../assets/dc-01/dns-forward-lookup-zone.png)

---

## Domain Controller Health Validation

### Objective

Verify domain controller health using the Microsoft `dcdiag` diagnostic tool.

### Procedure

```cmd
dcdiag /q
```

### Result

The captured command output returns to the prompt with no visible diagnostic errors.

`dcdiag /q` suppresses normal output and displays detected issues only. The captured result shows no reported issues in the visible output.

### Evidence

![DCDIAG Validation](../../assets/dc-01/dcdiag-validation.png)

---

## Group Policy Linking Validation

### Objective

Verify that the implemented Group Policy Objects are linked to the expected domain or OU locations.

### Result

Group Policy Management shows the following policy links:

| Scope | Linked GPO |
| --- | --- |
| `primesec.local` | `Default Domain Policy` |
| `primesec.local` | `GPO-Domain-Password-Policy` |
| `PRIMESEC/Workstations` | `GPO-Interactive-Logon-Notice` |
| `PRIMESEC/Workstations` | `GPO-Workstation-Security-Baseline` |
| `PRIMESEC/Workstations` | `GPO-Workstation-Windows-Update` |

This confirms that domain-level and workstation-level policy scopes are separated.

### Evidence

![Group Policy Linking](../../assets/dc-01/gpo-linking.png)

---

## Domain Password Policy Validation

### Objective

Verify the configured domain password and account lockout policy.

### Result

The `GPO-Domain-Password-Policy` evidence confirms the following settings:

| Setting | Value |
| --- | --- |
| Enforce password history | `24 passwords remembered` |
| Maximum password age | `90 days` |
| Minimum password age | `1 day` |
| Minimum password length | `12 characters` |
| Password complexity | `Enabled` |
| Reversible password encryption | `Disabled` |
| Account lockout threshold | `5 invalid logon attempts` |
| Account lockout duration | `15 minutes` |
| Reset account lockout counter | `15 minutes` |

### Evidence

![Domain Password Policy](../../assets/dc-01/gpo-password-policy.png)

---

## Interactive Logon Notice Validation

### Objective

Verify that the interactive logon notice GPO is configured.

### Result

The `GPO-Interactive-Logon-Notice` evidence confirms the configured logon notice.

| Setting | Value |
| --- | --- |
| Message title | `PrimeSec Infrastructure` |
| Message text | `Authorized Access Only. This workstation is managed by PrimeSec Infrastructure. Unauthorized use is prohibited and may be monitored.` |

### Evidence

![Interactive Logon Notice GPO](../../assets/dc-01/gpo-logon-notice.png)

---

## Workstation Security Baseline Validation

### Objective

Verify the workstation security baseline settings configured through Group Policy.

### Result

The `GPO-Workstation-Security-Baseline` evidence confirms the following settings:

| Setting | Value |
| --- | --- |
| Guest account status | `Disabled` |
| Do not display last signed-in user | `Enabled` |
| Turn off Microsoft Defender Antivirus | `Disabled` |

The Microsoft Defender policy means the GPO does not disable Microsoft Defender Antivirus.

### Evidence

![Workstation Security Baseline](../../assets/dc-01/gpo-security-baseline.png)

---

## Windows Update Policy Validation

### Objective

Verify the workstation Windows Update policy configured through Group Policy.

### Result

The `GPO-Workstation-Windows-Update` evidence confirms the following settings:

| Setting | Value |
| --- | --- |
| Configure Automatic Updates | `Enabled` |
| Automatic update mode | `4 - Auto download and schedule the install` |
| Scheduled install day | `0 - Every day` |
| Scheduled install time | `04:00` |
| No auto-restart with logged-on users | `Enabled` |

### Evidence

![Windows Update Policy](../../assets/dc-01/gpo-windows-update.png)

---

## Conclusion

Validation evidence confirms that `DC-01` is operating as the Active Directory domain controller, DNS authority for `primesec.local`, and Group Policy management point for the environment.

The captured evidence supports the configured domain, OU structure, DNS zone, domain controller health check, GPO linking model, and implemented GPO settings.
