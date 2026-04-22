# 🔍 NIST Incident Analysis: Phase 1 (Pre-Hardening)

## 1. Governance & Overview (ID.GV)
**Incident Type:** Passive/Active Network Reconnaissance  
**Target Asset:** Nextcloud Production Server (`192.168.1.103`)  
**Threat Actor:** Internal Actor (Kali Linux `192.168.1.x`)  

### Understanding the Attack Vector: Nmap Scanning
Nmap (Network Mapper) is a foundational tool used by both administrators and attackers. In this simulation, an **Aggressive Service Discovery Scan (`-A`)** was utilized. 
* **Port Discovery:** Identifies "open doors" on the server.
* **Service Fingerprinting:** Probes open ports to identify software versions (e.g., Apache 2.4).
* **OS Detection:** Uses TCP/IP stack behavior to guess the underlying Operating System (Ubuntu).

---

## 2. Detection (DE.AE-0002)
During the pre-hardening phase, the server was in a "Default Allow" state. The following telemetry was captured by the Wazuh SOC Manager.

### SOC Observation: Service Probe Flood
The Wazuh Agent on the Nextcloud server monitored the Apache access logs in real-time. Because the Nmap scan sends malformed packets to elicit a response, the web server generated hundreds of **400 Bad Request** errors.

**Evidence of Detection:**
![Wazuh Security Flags](Screenshots/wazuh-flags-nmap-scan.png)
*Figure 1: Wazuh Dashboard showing Rule ID 31101 (Web server 400 error code) triggered by Nmap service probing.*

---

## 3. Analysis & Vulnerability (RS.AN-0001)
At this stage, the scan was **successful**. The attacker gained the following intelligence:
* **Attack Surface:** Multiple TCP ports were identified as open.
* **Technology Stack:** The attacker successfully identified the presence of an Apache Web Server.

**Attacker Viewpoint:**
![Nmap Port Scan Result](Screenshots/nmap-port-scan.png)
*Figure 2: Terminal output from the attacker's perspective confirming the visibility of the target's internal services.*

---

## 4. Conclusion: Current Risk Profile
In its current state, the server is highly susceptible to **lateral movement**. An attacker within the network can freely map the entire service architecture, allowing them to choose specific exploits based on the identified software versions.

> [!CAUTION]
> **NIST Mitigation Requirement:** Transitioning to the **Protect (PR.AC-0003)** function is required to implement network access control and reduce the exposed attack surface.
