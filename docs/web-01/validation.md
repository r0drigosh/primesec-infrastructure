# WEB-01 Validation

## Purpose

This document records the validation procedures performed on WEB-01 to verify network connectivity, DNS functionality, service availability, firewall configuration and web service accessibility.

The objective of these tests is to confirm that WEB-01 is operating correctly as the Linux web server component of the PrimeSec Infrastructure environment.

Only completed validation procedures are documented within this file.

---

## Network Connectivity Validation

### Objective

Verify that WEB-01 can successfully communicate with external network destinations through FW-01.

### Procedure

The following command was executed:

```bash
ping -c 4 1.1.1.1
```

The test targeted Cloudflare's public DNS service to validate outbound network connectivity.

### Validation Results

The validation completed successfully.

Observed results:

- 4 packets transmitted
- 4 packets received
- 0% packet loss
- Successful round-trip communication

This confirms that WEB-01 can successfully reach external network resources through the configured gateway.

### Evidence

![Network Connectivity Validation](../../assets/web-01/ping-validation.png)

---

## DNS Resolution Validation

### Objective

Verify that WEB-01 can successfully resolve external domain names using the configured DNS infrastructure.

### Procedure

The following command was executed:

```bash
dig google.com
```

The test validated successful DNS query processing and hostname resolution.

### Validation Results

The validation completed successfully.

Observed results:

- DNS query returned successfully
- A record was resolved
- Query status returned `NOERROR`

This confirms that WEB-01 can perform DNS lookups required for normal operating system and application functionality.

### Evidence

![DNS Resolution Validation](../../assets/web-01/dns-validation.png)

---

## Apache Service Validation

### Objective

Verify that the Apache HTTP Server service is installed, running and operational.

### Procedure

The following command was executed:

```bash
systemctl status apache2
```

The service status output was reviewed to confirm operational state.

### Validation Results

The validation completed successfully.

Observed results:

- Apache service loaded successfully
- Apache service active and running
- Service startup completed successfully
- Apache process operational

This confirms that the web service is functioning correctly and available to serve web content.

### Evidence

![Apache Service Validation](../../assets/web-01/apache-status-validation.png)

---

## Firewall Validation

### Objective

Verify that the host-based firewall is enabled and enforcing the intended security policy.

### Procedure

The following command was executed:

```bash
sudo ufw status verbose
```

Firewall configuration and active rules were reviewed.

### Validation Results

The validation completed successfully.

Observed results:

- UFW active
- Default incoming policy set to deny
- Default outgoing policy set to allow
- SSH (22/TCP) permitted
- HTTP (80/TCP) permitted

This confirms that the firewall is operational and configured according to the documented security baseline.

### Evidence

![Firewall Validation](../../assets/web-01/firewall-validation.png)

---

## Service Startup Validation

### Objective

Verify that critical infrastructure services automatically start during system boot.

### Procedure

The following commands were executed:

```bash
systemctl is-enabled apache2
```

```bash
systemctl is-enabled ufw
```

Service startup configuration was reviewed for both Apache and UFW.

### Validation Results

The validation completed successfully.

Observed results:

- Apache service enabled
- UFW service enabled

This confirms that required services will automatically start following system reboots.

### Evidence

![Service Startup Validation](../../assets/web-01/service-startup-validation.png)

---

## Website Access Validation

### Objective

Verify that the Apache web service is accessible from the network and successfully serves the deployed landing page.

### Procedure

The web service hosted on WEB-01 was accessed using a web browser from the internal network.

The hosted landing page was reviewed to confirm successful page delivery and service availability.

### Validation Results

The validation completed successfully.

Observed results:

- Web page loaded successfully
- Apache service responding correctly
- Custom landing page displayed
- Infrastructure information presented as expected

This confirms that WEB-01 is successfully providing web services to clients on the network.

### Evidence

![Website Access Validation](../../assets/web-01/web-page-validation.png)

---

## Validation Summary

| Validation | Status |
|------------|---------|
| Network Connectivity | Passed |
| DNS Resolution | Passed |
| Apache Service | Passed |
| Firewall Configuration | Passed |
| Service Startup Configuration | Passed |
| Website Access | Passed |

---

## Conclusion

All planned validation procedures for WEB-01 were completed successfully.

Testing confirmed that the server can communicate with external networks, resolve DNS queries, operate the Apache HTTP service, enforce host-based firewall policies, automatically start required services during system boot and successfully deliver hosted web content.

Based on the completed validation activities, WEB-01 is operating as intended and fulfills its role as the Linux web server component of the PrimeSec Infrastructure Phase 1 environment.