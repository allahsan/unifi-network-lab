# 📶 UniFi WiFi Configuration

This document outlines the WiFi SSID structure, client distribution, band settings, and optimization configuration for the UniFi UDM Pro SE (UniFi OS 4.1.22) environment.

---

## 🛰️ SSIDs & VLAN Mapping

| SSID Name   | VLAN      | Band           | Broadcasting APs | Clients | Security |
|-------------|-----------|----------------|------------------|---------|----------|
| Home WAN    | VLAN 10   | 2.4GHz + 5GHz  | All              | 9       | WPA2     |
| Ping        | VLAN 20   | 2.4GHz + 5GHz  | All              | 7       | WPA2     |
| IoT_Hive    | VLAN 30   | 2.4GHz only    | All              | 11      | WPA2     |

📝 Notes:
- IoT_Hive is dedicated to 2.4GHz for legacy support.
- SSIDs are mapped to VLANs and broadcast on all APs.

---

## ⚙️ Wireless Band Configuration

| Frequency | Width Options | Status            | Notes                          |
|-----------|----------------|-------------------|--------------------------------|
| 2.4 GHz   | 20/40 MHz       | Enabled           | Channels 1–11 auto-selected    |
| 5 GHz     | 20/40/80/160 MHz| Enabled (80 MHz used) | DFS auto-handled         |
| 6 GHz     | Not in use      | Disabled          | Reserved for future expansion  |

---

## ⚙️ Optimization Settings

| Setting                   | Value         |
|---------------------------|---------------|
| Default WiFi Speeds       | Conservative  |
| Channel Width             | Auto (guided by Spectrum Optimizer) |
| Daily Spectrum Optimizer  | Enabled at 10 AM |
| Wireless Meshing          | Enabled       |
| Mesh Monitor              | Enabled       |
| UniFi Auto-Link           | Enabled       |
| WiFiman Support           | Enabled       |

🔄 **Channel selection is managed automatically** by UniFi’s built-in spectrum analysis and optimization engine. Admin has not statically assigned any channels.

---

## 📌 Summary

This WiFi design prioritizes:
- **Stability** for IoT (2.4GHz, simple spectrum)
- **Performance** for user devices (5GHz multi-width)
- **Low interference** via UniFi’s daily optimizer
- **Scalability** for future 6GHz support

---

_Last updated: May 2025_
