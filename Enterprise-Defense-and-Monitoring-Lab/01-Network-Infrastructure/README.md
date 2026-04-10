# 🛡️ Network Infrastructure: pfSense Firewall

## Objective
To design and implement a segmented network architecture that isolates the SOC management tools and target servers from the public internet, using a dual-homed firewall as the secure gateway.

---

## 🌐 Network Topology
The environment is divided into two distinct security zones:

1. **WAN (External):** Bridged to the physical host network for controlled internet access (Updates/Downloads).
2. **SOC-LAN (Internal):** A 192.168.1.0/24 private subnet hosting the Wazuh Manager, Windows Workstation, and Nextcloud Server.

### IP Address Schema
| Device | Interface | IP Address |
| :--- | :--- | :--- |
| **pfSense Gateway** | SOC-LAN | `192.168.1.1` |
| **Wazuh Manager** | SOC-LAN | `192.168.1.102` |
| **Windows 11 WS** | SOC-LAN | `192.168.1.101` |
| **Nextcloud Server** | SOC-LAN | `192.168.1.4` |

---

## 🔒 Security Hardening & Firewall Rules
To maintain a "Zero Trust" posture, the following rules were implemented on the pfSense interface:

* **DNS/NTP Services:** Allowed from SOC-LAN to the Gateway to ensure time sync (critical for log timestamps).
* **Restricted Outbound:** Only specific management ports are allowed out; all other traffic is blocked by default (Implicit Deny).
* **Anti-Lockout:** Configured to ensure management access remains available from the primary workstation.

---

## 🖼️ Evidence (Batch Upload Pending)
* `[Placeholder: pfSense-Interfaces.png]` - View of the WAN/LAN assignment.
* `[Placeholder: pfSense-Firewall-Rules.png]` - Screenshot of the LAN rule-base.
* `[Placeholder: pfSense-DHCP-Leases.png]` - Confirmation of static IP assignments for the lab VMs.
