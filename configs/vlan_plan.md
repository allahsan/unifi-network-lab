# 🌐 VLAN Plan

This document outlines the complete VLAN segmentation plan in use on the UDM Pro SE (UniFi OS 4.1.22). Each VLAN is assigned based on function and level of isolation required, enforced by custom firewall rules.

---

## 🗂️ VLAN Overview

| VLAN Name   | VLAN ID | Purpose                             |
|-------------|---------|-------------------------------------|
| management  | 1       | UniFi Controller, switches, APs     |
| homewan     | 10      | Main devices: phones, PCs, TVs      |
| homeguest   | 20      | Guest WiFi, isolated                |
| homeIOT     | 30      | Smart devices (Echo, etc.)          |
| homeIOTld   | 40      | Locked-down smart devices           |
| homeserver  | 86      | Servers: Proxmox, PBS, file share   |

---

## 📡 Inter-VLAN Rules

| From         | To            | Action | Notes                                      |
|--------------|---------------|--------|--------------------------------------------|
| homewan      | homeserver    | ✅ Allow | Access media and file shares               |
| homewan      | management    | ❌ Deny  | Can't reach controller or switches         |
| homeIOT      | Any           | ❌ Deny  | Total isolation except for mDNS            |
| homeIOTld    | Any           | ❌ Deny  | Locked down even tighter                   |
| VPN          | homeserver    | ✅ Allow | Remote RDP, media, SSH                     |
| VPN          | UDM GUI       | ❌ Deny  | Blocks access to UniFi interfaces          |
| management   | UDM           | ✅ Allow | Controller/switches to UDM communication   |

---

## Notes

- mDNS and IGMP allowed in homeIOT and homeIOTld for casting and discovery.
- DHCP enabled for all VLANs.
- VLAN 1 and 86 are not broadcast over WiFi.

_Last updated: May 2025_
