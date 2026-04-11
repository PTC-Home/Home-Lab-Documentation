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

---

### Installing and updating Ubuntu Server
For prepreation of working on the installation of Nextcloud, I updated the Ubuntu server and opted out of the snapshot of a premade Nextcloud vm.

---

### Phase 1: Environment & Database Hardening
Before deploying the application, the underlying LAMP stack was hardened to reduce the attack surface.

**Actions Taken:**
1. **Service Verification:** Confirmed `apache2` and `mariadb` status via `systemctl`.
2. **Database Hardening:** Executed `mysql_secure_installation` to:
    * Disable remote root login.
    * Remove anonymous user accounts.
    * Purge the default 'test' database.
3. **Module Optimization:** Installed specific PHP extensions (`php-imagick`, `php-gmp`, `php-bcmath`) required for enterprise-grade file encryption and processing.

---
