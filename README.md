# 🏠 Advanced Home Network Infrastructure

Welcome to the documentation of my home network project. This setup is built on the **UDM Pro SE** running **UniFi OS 4.1.22**, simulating a secure, enterprise-style infrastructure for virtualization, segmentation, and secure remote access.

---

## 🚩 Project Objectives

- 🧠 Implement enterprise-grade VLAN segmentation and firewalling  
- 🔐 Secure access via **WireGuard VPN** (with DDNS)  
- 📊 Monitor UniFi, Proxmox, and network stats using **Grafana + InfluxDB + UniFi Poller**  
- 💾 Enable reliable backup and recovery via **Proxmox Backup Server (PBS)**  
- 🧰 Build real-world IT documentation and system architecture  

---

## 📂 Repository Structure

```plaintext
📁 unifi-network-lab/
├── README.md
├── network_diagram.png
├── 📁 configs/
│   ├── vlan_plan.md
│   ├── firewall_rules.md
│   └── vpn_config.md
├── 📁 monitoring/
│   ├── unifi_poller_setup.md
│   ├── grafana_dashboards.json
│   └── influxdb_setup.md
├── 📁 backup_and_restore/
│   ├── proxmox_pbs_guide.md
│   └── restore_from_crash.md
├── 📁 automation/
│   └── wireguard_ddns_sop.md
└── LICENSE
