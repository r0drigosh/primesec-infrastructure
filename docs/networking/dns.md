## DNS Configuration

fw-01 provides DNS services using Unbound DNS.

The internal domain is:

- primesec.internal

External DNS queries are forwarded to:

- 1.1.1.1
- 1.0.0.1

web-01 is configured to use fw-01 (10.10.10.1) as its primary DNS server.

## Troubleshooting

During the deployment, DNS queries returned SERVFAIL errors.

The issue was caused by an incomplete Unbound forwarding configuration.

To resolve the problem:

- Cloudflare DNS servers were configured
- Query Forwarding was enabled
- web-01 was updated to use fw-01 as its DNS server

DNS functionality was verified using dig and resolvectl.