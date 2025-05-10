# 🌐 Network & VLAN Configuration

This document outlines the configured VLANs, subnet structure, multicast behavior, and UniFi switch-level settings in this home lab running on UDM Pro SE (UniFi OS 4.1.22).

---

## 🧾 VLAN & Subnet Overview

| VLAN Name   | VLAN ID | Subnet        | IP Leases | Purpose                            |
|-------------|---------|---------------|-----------|------------------------------------|
| management  | 1       | /29           | 1         | UniFi controllers and switches     |
| homewan     | 10      | /24           | 15        | Primary user network               |
| homeguest   | 20      | /24           | 4         | Guest WiFi (isolated internet)     |
| homeIOT     | 30      | /24           | 11        | Smart home devices                 |
| homeserver  | 86      | /24           | 0         | Proxmox, PBS, NAS (static IP only) |
| homeIOTld   | 40      | /24           | 7         | Locked-down smart/unknown devices  |

---

## 📡 Multicast & mDNS Configuration

| Feature           | Enabled For                            | Purpose                               |
|------------------|-----------------------------------------|----------------------------------------|
| mDNS              | homeIOT, homeIOTld                      | Allows local discovery (e.g. casting)  |
| IGMP Snooping     | All VLANs                               | Efficient multicast control            |
| Forward Unknown   | Drop                                    | Prevents multicast flooding            |

🔍 *Fast Leave, Querier Switch options remain default/disabled.*

---

## 🔒 Global Switch Settings

| Setting                     | Status     |
|-----------------------------|------------|
| Spanning Tree Protocol      | RSTP       |
| Rogue DHCP Server Detection | ✅ Enabled |
| Jumbo Frames                | ❌ Disabled|
| Flow Control                | ❌ Disabled|
| 802.1X Control              | ❌ Disabled|

---

## 🧠 Notes

- **Rogue DHCP detection** prevents device spoofing across VLANs
- **homeserver** VLAN is fully static IP-based and not listed in DHCP leases
- **management VLAN** is isolated from end-user access via firewall rules
- All VLANs routed by UDM (“Dream Machine” shown as router)

---

_Last updated: May 2025_
