# 🔥 Firewall Rules

This document outlines the firewall rule structure used in the UDM Pro SE (UniFi OS 4.1.22) to enforce VLAN isolation, allow selective communication, and secure the overall network.

Firewall rules in UniFi are enforced at the interface level (LAN IN, LAN OUT, etc.).

---

## 🚦 Core Rule Strategy

| Rule Name                  | Source VLAN     | Destination VLAN | Action | Purpose                                      |
|---------------------------|------------------|------------------|--------|----------------------------------------------|
| Block IoT to All          | homeIOT (30)     | Any              | ❌ Deny | Prevent smart devices from reaching LAN      |
| Block IoTLD to All        | homeIOTld (40)   | Any              | ❌ Deny | Fully isolated IoT devices                   |
| Allow HomeWAN to Server   | homewan (10)     | homeserver (86)  | ✅ Allow | Access to Proxmox, File Server, etc.         |
| Block HomeWAN to MGMT     | homewan (10)     | management (1)   | ❌ Deny | Prevent access to UniFi controllers          |
| Allow MGMT to Gateway     | management (1)   | Gateway          | ✅ Allow | For APs, switches to talk to UDM             |
| Allow VPN to Server VLAN  | VPN              | homeserver (86)  | ✅ Allow | Limited remote access to internal services   |
| Block VPN to UDM GUI      | VPN              | Gateway/UDM      | ❌ Deny | Restrict UI/SSH control from VPN             |
| Allow mDNS + IGMP         | homeIOT          | Multicast        | ✅ Allow | Enable casting (mDNS, AirPrint, etc.)        |

---

## 🛑 Default Deny Policy

- All interfaces follow a **deny-by-default** model.
- VLAN-to-VLAN traffic is blocked unless explicitly allowed.
- Rules are applied at **LAN IN** and **VPN IN** levels.

---

## 🔐 Special Notes

- **VPN** is strictly scoped to internal services — never the UI.
- **IoT VLANs** cannot access anything but the internet (and multicast).
- **Management VLAN** is isolated except for switch/controller access.

---

_Last updated: May 2025_
