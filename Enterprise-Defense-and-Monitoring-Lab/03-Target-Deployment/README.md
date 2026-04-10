#  Target Deployment: Nextcloud "Crown Jewel"

## Objective
To deploy a functional Private Cloud instance (Nextcloud) to serve as the primary "victim" or target for security monitoring and offensive simulation. This server represents an enterprise data asset that must be protected and audited.

---

##  Server Architecture (LAMP Stack)
* **OS:** Ubuntu 24.04 LTS
* **Web Server:** Apache2
* **Database:** MariaDB (SQL)
* **Runtime:** PHP 8.3
* **Network IP:** `192.168.1.103` (Static)

---

##  Hardening Measures (Phase 1)
* **Database Isolation:** Manual MariaDB configuration with dedicated non-root users.
* **Firewall Logic:** Integrated with pfSense to allow only HTTP/HTTPS and SSH from the Management Workstation.
* **Agent Integration:** Deployment of the Wazuh Agent for File Integrity Monitoring (FIM).

---

##  Evidence (Batch Upload Pending)
* `[Placeholder: Nextcloud-Service-Status.png]` - Showing Apache and MariaDB running.
* `[Placeholder: Nextcloud-Dashboard-Login.png]` - The final functional Nextcloud GUI.
🛠️ Professional Touch
