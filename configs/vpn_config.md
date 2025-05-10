# 🔐 WireGuard VPN Configuration (UniFi)

This document captures the full configuration of the native WireGuard VPN server managed by the UDM Pro SE (UniFi OS 4.1.22), as visible in the UniFi Controller interface.

---

## 🎯 Overview

- **VPN Type:** WireGuard
- **Interface:** WAN1
- **Use Alternate Address for Clients:** ✅ Enabled
- **DNS Server:** Auto (managed by UDM)
- **Client Allocation Mode:** Manual

---

## 🌐 VPN Server Network Settings

| Setting         | Value                    |
|-----------------|--------------------------|
| Gateway IP      | `172.27.27.1`            |
| Subnet Mask     | `/24`                    |
| IP Range        | `172.27.27.1 - 172.27.27.254` |
| Usable IPs      | 253                      |
| Broadcast IP    | `172.27.27.255`          |
| DNS Server      | Auto (via UDM DHCP)      |

---

## 👥 WireGuard Clients

Each client is assigned a static IP from the VPN subnet and authorized via the controller.

| Client Name   | Assigned IP     |
|---------------|-----------------|
| Client 1      | `172.27.27.X`   |
| Client 2      | `172.27.27.X`   |
| Client 3      | `172.27.27.X`   |
| Client 4      | `172.27.27.X`   |
| Client 5      | `172.27.27.X`   |
| Client 6      | `172.27.27.X`   |

🧠 You manage clients directly through the UniFi Controller interface under VPN settings.

---

## 🔄 Alternate IP Address Feature

☑️ **Enabled**  
When activated, clients connect using an alternate domain/IP (typically a DDNS address). This ensures stability when your WAN IP changes.

Example:
- `yourdomain.duckdns.org`

---

## 🔐 Firewall & Routing Notes

- VPN clients are **restricted from accessing UniFi GUI and management ports**
- VLAN-level access is scoped via firewall rules (e.g., VPN → VLAN 86 only)
- UniFi’s firewall rules ensure inter-VLAN isolation remains enforced
- `LAN IN` and `VPN IN` rules apply

---

## ✅ Use Case Summary

| Feature                                | Enabled |
|----------------------------------------|---------|
| Secure remote access                   | ✅       |
| DDNS-friendly with alternate address   | ✅       |
| Block GUI/SSH via VPN                  | ✅       |
| Multi-client support                   | ✅       |

---

_Last updated: May 2025_
