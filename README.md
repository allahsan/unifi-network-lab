# 🏠 UniFi Network Lab

Welcome to my home lab project — a fully segmented, monitored, and secure network built using the **UDM Pro SE (UniFi OS 4.1.22)**. This setup simulates enterprise-grade architecture for learning, documentation, and real-world practice.

---

## 🚩 Project Goals

- 🧱 Learn and apply real-world VLAN segmentation
- 🔐 Secure access using WireGuard + DDNS
- 📊 Monitor network and server activity with Grafana + InfluxDB
- 🔁 Back up and restore with Proxmox Backup Server
- 🧰 Document infrastructure like a real system admin

---

## 📂 Folder Structure

📁 unifi-network-lab/
├── README.md
├── 📁 configs/
│ ├── vlan_plan.md
│ ├── firewall_rules.md
│ └── vpn_config.md
├── 📁 automation/
│ └── wireguard_ddns_sop.md
├── 📁 monitoring/
│ ├── unifi_poller_setup.md
│ ├── influxdb_setup.md
│ └── grafana_dashboards.json
├── 📁 backup_and_restore/
│ ├── proxmox_pbs_guide.md
│ └── restore_from_crash.md
└── LICENSE

yaml
Copy
Edit

---

## 🧱 Network Layout

### 🔹 VLANs

| Name        | VLAN ID | Purpose                           |
|-------------|---------|-----------------------------------|
| management  | 1       | UniFi Controller, switches, APs   |
| homewan     | 10      | Personal devices (TVs, phones)    |
| homeguest   | 20      | Internet-only guest devices       |
| homeIOT     | 30      | Smart home devices (Echo, TVs)    |
| homeIOTld   | 40      | Locked-down IoT                   |
| homeserver  | 86      | Proxmox, PBS, File servers        |

📑 Full VLAN logic: [configs/vlan_plan.md](./configs/vlan_plan.md)

---

### 🔹 WiFi Networks (SSID → VLAN)

| SSID        | VLAN       | Devices          | Notes                        |
|-------------|------------|------------------|------------------------------|
| Home WAN    | VLAN 10    | All personal use | mDNS enabled for casting     |
| Ping        | VLAN 20    | Guest phones     | Isolated, no LAN access      |
| IoT_Hive    | VLAN 30    | Echo, cameras    | mDNS allowed only            |

---

## 🔐 Firewall Logic

| Source VLAN  | Destination | Action | Description                              |
|--------------|-------------|--------|------------------------------------------|
| homeIOT      | Any         | ❌     | Blocks IoT from accessing LAN            |
| homewan      | homeserver  | ✅     | Allows RDP/SMB access                    |
| VPN          | homeserver  | ✅     | Access to Proxmox from anywhere          |
| VPN          | UDM GUI     | ❌     | Remote GUI/SSH access blocked            |

📑 Full firewall rules: [configs/firewall_rules.md](./configs/firewall_rules.md)

---

## 🌐 VPN & Remote Access

- WireGuard VPN runs on a Debian VM inside VLAN 86
- Clients routed only to `homeserver` VLAN (172.27.27.x)
- DDNS powered by DuckDNS

📑 Setup steps: [automation/wireguard_ddns_sop.md](./automation/wireguard_ddns_sop.md)

---

## 📊 Monitoring Stack

| Tool         | Function                  |
|--------------|---------------------------|
| Grafana      | Dashboards & visualization|
| InfluxDB     | Stores UniFi + Proxmox data|
| UniFi Poller | Pulls stats from UDM Pro SE|

📑 Setup guides in `/monitoring/`

---

## 💾 Backups

- Full VM backups handled by **Proxmox Backup Server**
- Restore procedures tested from disk-level crashes

📑 Restore SOP: [backup_and_restore/restore_from_crash.md](./backup_and_restore/restore_from_crash.md)

---

## ✍️ Author

**Allfin Ahsan**  
System Administrator | Cybersecurity Learner  
Documenting everything I build, so I can learn deeper and help others do the same.

---
