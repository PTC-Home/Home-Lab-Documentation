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

###  Hardening Measures (Phase 1)
* **Database Isolation:** Manual MariaDB configuration with dedicated non-root users.
* **Firewall Logic:** Integrated with pfSense to allow only HTTP/HTTPS and SSH from the Management Workstation.
* **Agent Integration:** Deployment of the Wazuh Agent for File Integrity Monitoring (FIM).

---

###  Evidence (Batch Upload Pending)
* `[Placeholder: Nextcloud-Service-Status.png]` - Showing Apache and MariaDB running.
* `[Placeholder: Nextcloud-Dashboard-Login.png]` - The final functional Nextcloud GUI.
Professional Touch

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

### Phase 2: Database & File System Configuration
A dedicated MariaDB database was provisioned using the Principle of Least Privilege (PoLP).

**Key Actions:**
* **Database Isolation:** Created `nextcloud_db` to ensure data segregation from system-level tables.
* **Service Account:** Provisioned a non-root user (`nc_admin`) with scoped privileges limited strictly to the application database.
* **Permission Hardening:** Configured recursive ownership of the `/var/www/html/nextcloud` directory to the `www-data` service account, preventing unauthorized file execution by other system users.

### File System Permissions & Security
To ensure the application can function while adhering to the **Principle of Least Privilege**, recursive ownership was applied to the web root.

**Command:**
```bash
sudo chown -R www-data:www-data /var/www/html/nextcloud/
```

---

### Phase 3: Telemetric Integration (Wazuh Agent Deployment)
To transform the standalone Nextcloud server into a monitored "Target" within the SOC, the Wazuh security agent was deployed to provide real-time visibility.

**Execution Steps:**
1. **Dependency Verification:** Confirmed `curl` and `wget` were present for remote package retrieval.
2. **Agent Provisioning:** Utilized the Wazuh Manager's deployment wizard to generate a unique installation string for the Ubuntu 24.04 (DEB amd64) architecture.
3. **Manager Alignment:** Pointed the agent to the Manager IP (`192.168.1.102`) and assigned the hostname `Nextcloud-Server-01`.
4. **Service Persistence:** Enabled the agent via `systemctl` to ensure monitoring survives system reboots.

> [!TIP]
> **Security Outcome:**
> The server now provides active File Integrity Monitoring (FIM). Any unauthorized changes to sensitive Nextcloud configuration files (like `config.php`) will trigger a Level 7+ alert on the Wazuh dashboard.
