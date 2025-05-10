# 🌐 Internet / WAN Configuration (UDM Pro SE)

This document describes the WAN (Internet) configuration used on the UniFi UDM Pro SE, including interface details, performance, DNS, dynamic IP management (DDNS), and IPv4 setup.

---

## 🔌 WAN Interface

| Field         | Value                |
|---------------|----------------------|
| Interface     | **Primary (WAN1)**   |
| Device        | Dream Machine        |
| Port Used     | Port 9 (2.5 GbE)     |
| VLAN Tagging  | Not Enabled          |

---

## ⚡ ISP Speed Configuration

| Direction | Configured Speed |
|-----------|------------------|
| Download  | 1100 Mbps        |
| Upload    | 300 Mbps         |
| Mode      | Manual           |

This speed is manually defined for accurate DPI (Deep Packet Inspection) and bandwidth reports.

---

## 🌍 Dynamic DNS (DDNS)

| Provider | Hostname               | Status |
|----------|------------------------|--------|
| DuckDNS  | `yourdomain.duckdns.org` | ✅ Active |

> 🧠 This allows WireGuard VPN and remote services to resolve your public IP even when your ISP changes it.

---

## 🌐 IPv4 Configuration

| Setting             | Value          |
|---------------------|----------------|
| Connection Type     | DHCPv4         |
| DHCP Client Options | (none defined) |
| Primary DNS Server  | `1.1.1.1`      |
| Secondary DNS Server| `8.8.8.8`      |
| Auto DNS            | Disabled       |

> Manually using Cloudflare (1.1.1.1) and Google DNS (8.8.8.8) for better performance and privacy.

---

## 🚫 IPv6 Configuration

| Setting         | Value     |
|------------------|-----------|
| IPv6 Mode        | Disabled  |

No IPv6 is used on this WAN connection, reducing surface area and complexity for home lab use.

---

## 🛠 Advanced Options (Disabled by default)

- Smart Queues: ❌  
- IGMP Proxy: ❌  
- UPnP: ❌  
- MAC Address Cloning: ❌  
- DHCP CoS: ❌

These features are left disabled to maintain a controlled, secure, and manually managed network environment.

---

_Last updated: May 2025_
