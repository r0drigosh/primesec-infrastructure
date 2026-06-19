# Group Policy Implementation

## Purpose

Group Policy was implemented to provide centralized configuration management across the PrimeSec Infrastructure environment.

By leveraging Active Directory Group Policy Objects (GPOs), administrative controls can be applied consistently to domain-joined systems without requiring manual configuration on individual endpoints. This approach improves operational efficiency, reduces configuration drift, and enables standardized security controls across the environment.

The implementation focuses on a small set of practical policies that reflect common enterprise administration practices while maintaining simplicity appropriate for a small infrastructure deployment.

---

## Group Policy Strategy

The Group Policy design follows a layered approach that separates domain-wide controls from workstation-specific configuration.

Domain-level policies are used to enforce identity and authentication requirements that apply to all domain accounts. Workstation-level policies are linked to the Workstations Organizational Unit and are used to manage endpoint security and operating system behavior.

This design provides:

- Centralized administration
- Consistent configuration management
- Targeted policy deployment
- Reduced administrative overhead
- Simplified future expansion

The Organizational Unit structure enables policies to be applied only where required, avoiding unnecessary configuration of unrelated systems while maintaining a clear administrative model.

### Evidence

![Group Policy Linking Strategy](../../assets/dc-01/gpo-linking.png)

---

## Domain Password Policy

The domain password policy establishes centralized credential requirements for all domain accounts.

The policy enforces:

- Password complexity requirements
- Minimum password length of 12 characters
- Password history of 24 remembered passwords
- Maximum password age of 90 days
- Minimum password age of 1 day
- Account lockout after 5 failed logon attempts
- Account lockout duration of 15 minutes
- Reset counter after 15 minutes
- Reversible password encryption disabled

These controls help reduce the risk of weak credentials, password reuse, and unauthorized access attempts.

### Business Justification

Strong authentication controls are a fundamental security requirement in enterprise environments. Centralized password policies help protect user accounts from brute-force attacks while promoting consistent credential management practices throughout the domain.

### Evidence

![Domain Password Policy](../../assets/dc-01/gpo-password-policy.png)

---

## Workstation Security Baseline

A workstation security baseline was implemented to establish a consistent configuration standard for domain-joined endpoints.

The policy includes:

- Guest account disabled
- Last signed-in user information hidden
- Centrally managed workstation security settings
- Standardized endpoint configuration

The objective is to ensure that workstations operate according to a defined baseline rather than relying on individual local configurations.

### Business Justification

Standardized workstation configuration reduces the likelihood of security misconfigurations and simplifies ongoing administration. Centralized baseline management also improves consistency across endpoints and supports scalable workstation administration.

### Evidence

![Workstation Security Baseline](../../assets/dc-01/gpo-security-baseline.png)

---

## Windows Update Management

A dedicated Windows Update policy was implemented to centrally manage operating system updates on domain-joined workstations.

The policy configures:

- Automatic Updates enabled
- Automatic download and installation
- Daily update deployment schedule
- Scheduled installation at 04:00
- Prevention of automatic restarts while users are logged on

This approach allows update deployment to be managed centrally while minimizing disruption to users.

### Business Justification

Consistent patch management is essential for maintaining endpoint security and system stability. Centralized update configuration helps ensure that workstations receive security updates in a predictable manner while reducing administrative effort and operational disruption.

### Evidence

![Windows Update Policy](../../assets/dc-01/gpo-windows-update.png)

---

## Interactive Logon Notice

An interactive logon notice was deployed to display a security and authorized-use warning before user authentication.

The policy presents users with an informational banner containing an authorized access statement and organizational notice.

The implementation demonstrates centralized deployment of security messaging through Group Policy and reflects a commonly adopted enterprise practice.

### Business Justification

Logon banners help reinforce acceptable use expectations and provide notice that systems are intended for authorized users only. While the legal requirements vary between organizations, the use of security notices remains a common administrative control within enterprise environments.

### Policy Configuration

![Interactive Logon Policy](../../assets/dc-01/gpo-logon-notice.png)

### User Experience Validation

![Interactive Logon Notice](../../assets/ws-01/interactive-logon-notice.png)

---

## Exported Policy Reports

In addition to the implementation screenshots included throughout this document, Group Policy reports were exported directly from the Group Policy Management Console.

These reports provide detailed configuration information for each deployed policy and serve as implementation evidence and configuration references for the environment.

Available reports include:

- [GPO-Domain-Password-Policy](../../reports/gpo/GPO-Domain-Password-Policy.html)
- [GPO-Interactive-Logon-Notice](../../reports/gpo/GPO-Interactive-Logon-Notice.html)
- [GPO-Workstation-Security-Baseline](../../reports/gpo/GPO-Workstation-Security-Baseline.html)
- [GPO-Workstation-Windows-Update](../../reports/gpo/GPO-Workstation-Windows-Update.html)

The exported reports provide a detailed view of policy scope, configuration settings, security filtering, and link assignments. They supplement the documentation by providing a reproducible reference for the deployed Group Policy configuration.

---

## Security Benefits

The Group Policy implementation provides several operational and security benefits.

### Centralized Administration

Configuration changes can be deployed from a single management point rather than being applied individually to each endpoint.

### Reduced Configuration Drift

Policies help ensure that workstations remain aligned with organizational standards and reduce inconsistencies introduced through manual configuration.

### Consistent Workstation Security

Security settings are applied uniformly across managed systems, improving predictability and reducing the likelihood of endpoint misconfiguration.

### Improved Operational Efficiency

Administrative effort is reduced through centralized management, enabling common configuration tasks to be performed at the domain level.

### Simplified Policy Management

The Organizational Unit structure and targeted policy linking model provide a scalable foundation for future policy expansion and infrastructure growth.

---

## Design Summary

Group Policy was implemented as the primary mechanism for centralized configuration management within the PrimeSec Infrastructure environment.

The deployment includes domain-wide authentication controls, workstation security baselines, centralized Windows Update management, and an interactive logon notice. Together, these policies demonstrate practical enterprise administration concepts including identity management, policy enforcement, endpoint standardization, and centralized operational control.

The implementation provides a maintainable and scalable foundation for future infrastructure growth while demonstrating core Active Directory and Group Policy administration capabilities relevant to systems administration, infrastructure management, and enterprise IT operations.