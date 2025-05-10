# 🌍 Dynamic DNS (DDNS) Configuration — DuckDNS (UDM Pro SE)

This document outlines the exact DDNS configuration used on the UDM Pro SE (UniFi OS 4.1.22) for reliable remote access via DuckDNS. This configuration enables persistent DNS mapping to a dynamic WAN IP.

---

## 🧾 DDNS Provider Details

| Field     | Value                 |
|-----------|-----------------------|
| Service   | DuckDNS               |
| Hostname  | `your-subdomain.duckdns.org` |
| Username  | DuckDNS token         |
| Password  | DuckDNS token         |
| Server URL| `www.duckdns.org/update?domains=%h&token=%p&ip=%i` |


```plaintext
www.duckdns.org/update?domains=%h&token=%p&ip=%i
