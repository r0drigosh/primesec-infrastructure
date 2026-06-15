# Tailscale Integration

## Overview

Tailscale is used to provide secure remote access to the PrimeSec infrastructure.

## Configuration

- OPNsense Tailscale plugin installed
- Tailscale interface assigned
- Firewall rules created for management access
- Subnet advertisement configured for 10.10.10.0/24

## Advertised Routes

| Subnet |
|----------|
| 10.10.10.0/24 |

## Troubleshooting

### Firmware Upgrade Issue

After an OPNsense firmware upgrade, Tailscale connectivity stopped working correctly.

#### Symptoms

- Tailscale service inactive after reboot
- Tailscale interface disabled
- Loss of access through Tailscale IP
- Advertised subnet routes unavailable

#### Root Cause

The firmware upgrade affected the Tailscale integration configuration.

The Tailscale interface was no longer enabled and subnet advertisement settings required reconfiguration.

#### Resolution

- Verified service startup configuration
- Re-enabled Tailscale interface
- Recreated firewall rules
- Reconfigured subnet advertisement
- Validated connectivity through Tailscale

#### Lessons Learned

Always validate VPN services and interface assignments after firmware upgrades.