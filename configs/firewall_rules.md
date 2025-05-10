# 🔥 UniFi Firewall Configuration

This document captures the full firewall ruleset enforced on the UDM Pro SE (UniFi OS 4.1.22), including inter-VLAN blocking, VPN scoping, and management protection.

---

## 🚦 Core LAN IN Rules

| Rule Name                          | Action | From VLAN       | To VLAN / Zone      | Purpose                                      |
|-----------------------------------|--------|------------------|----------------------|----------------------------------------------|
| Block UniFi GUI from VPN          | ❌     | VPN              | Gateway              | Block VPN from reaching UDM UI/SSH           |
| Allow Home Printer to VLAN        | ✅     | Internal         | Internal             | Allow cross-device printing within VLAN 10   |
| Allow HomeServer to HomeWAN       | ✅     | homeserver       | homewan              | Allow casting, RDP, media                    |
| Allow HomeWAN to HomeServer       | ✅     | homewan          | homeserver           | Allow access to Proxmox, PBS                 |
| Allow Management to UDM           | ✅     | management        | Gateway              | Allow UniFi controller visibility            |
| Allow WINS to homeIOTld           | ✅     | Internal         | homeIOTld            | Discovery/casting exceptions                 |

---

## 🛑 Isolation & Blocking Rules

| Rule Name                          | Action | Source Zone     | Destination Zone    | Description                                 |
|-----------------------------------|--------|------------------|----------------------|----------------------------------------------|
| Block HomeGuest to LAN            | ❌     | homeguest        | Internal             | Blocks guest VLAN from local access         |
| Block homeIOT to LAN              | ❌     | homeIOT          | 5 Networks           | Full IoT isolation                          |
| Block homeIOTld to LAN            | ❌     | homeIOTld        | 3 Networks           | Maximum lockdown for restricted devices     |
| Block homeIOTld to LANIO + WAN    | ❌     | homeIOTld        | 2 Networks           | Block Internet + Inter-VLAN                 |
| Block HomeServer to LAN           | ❌     | homeserver       | 3 Networks           | Prevent lateral movement from server VLAN   |
| Block HomeWAN to LAN (Except Servers)| ❌  | homewan          | 3 Networks           | Prevent personal devices from other VLANs   |
| Block UniFi GUI from LAN          | ❌     | 5 Networks        | Gateway              | Blocks management access from end-users     |

---

## 🔐 VPN IN Rules

| Rule Name                          | Action | Source Zone     | Destination Zone    | Purpose                                      |
|-----------------------------------|--------|------------------|----------------------|----------------------------------------------|
| Block VPN to LAN (Exceptions-only)| ❌     | VPN              | 5 Networks           | Restrict VPN access to only defined VLANs    |
| VPN devices to VPN devices        | ✅     | VPN              | VPN                  | Allow intra-VPN traffic                      |

---

## 🌐 External Access Rules

| Rule Name                          | Action | Protocol | Source Zone | Destination | Port |
|-----------------------------------|--------|----------|-------------|-------------|------|
| Allow Direct Remote Connection    | ✅     | TCP      | External    | Gateway     | 443  |
| Allow Management VLAN Access (Remote)| ✅ | All      | Internal    | Internal    | Any  |

---

## 🧠 IPv6 Rules

| Rule Name                          | Action | Protocol | Zone     | Purpose             |
|-----------------------------------|--------|----------|----------|----------------------|
| Allow Neighbor Advertisements     | ✅     | ICMPv6   | External | IPv6 discovery       |
| Allow Neighbor Solicitations      | ✅     | ICMPv6   | External | IPv6 gateway checks  |

---

## 🔄 Miscellaneous

| Rule Name             | Action | Purpose                                   |
|----------------------|--------|-------------------------------------------|
| Allow Return Traffic | ✅     | Maintains stateful connections            |
| Allow WireGuard VPNs | ✅     | Enables external WG peer connections      |
| Allow mDNS           | ✅     | Multicast service discovery               |
| Block Invalid Traffic| ❌     | Blocks malformed or spoofed packets       |
| Isolated Networks    | ❌     | Prevents cross-talk between isolated VLANs|
| Allow All Traffic    | ✅     | (Default allow - likely overridden)       |
| Block All Traffic    | ❌     | (Failsafe catch-all)                      |

---

## 🔐 Notes

- All rules are processed top-down — most restrictive rules placed first.
- Exceptions for casting, printing, and management access are granularly defined.
- VLAN isolation is strongly enforced at both LAN IN and VPN IN levels.
- Default deny approach is applied where appropriate.

---

_Last updated: May 2025_
