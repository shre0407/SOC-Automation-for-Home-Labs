### Project Requirements for GitHub SOC Automation Project (Bachelor's Level)  

#### **1. Wazuh Agent**  
**Hardware Requirements:**  
- **Host System:** Windows 10 PC (64-bit).  
- **CPU:** Minimum 2-core processor (Intel/AMD).  
- **RAM:** 4 GB minimum.  
- **Storage:** 50 GB free disk space for log retention.  

**Software Configuration:**  
- **OS:** Windows 10 Pro/Enterprise (64-bit).  
- **Wazuh Agent:** Latest stable version installed and registered with the Wazuh Manager.  
- **Log Sources:** Enable collection of Windows Event Logs (Security, System, Application), Sysmon logs (if applicable), and application-specific logs.  
- **Network:** Configure firewall rules to allow outbound communication to Wazuh Manager on port `1514/udp` (encrypted).  

---

#### **2. Wazuh Manager**  
**Hardware Requirements:**  
- **Cloud Server:** Ubuntu 22.04 LTS (AWS/Azure/GCP or equivalent).  
- **CPU:** 4-core processor (recommended).  
- **RAM:** 8 GB minimum.  
- **Storage:** 100 GB SSD (for log storage and analysis).  

**Software Configuration:**  
- **OS:** Ubuntu 22.04 LTS.  
- **Wazuh Manager:** Latest version installed with Elastic Stack integration (Elasticsearch, Logstash, Kibana).  
- **Ruleset:** Preloaded with OOTB security rules and custom rules for home lab threats (e.g., brute-force attacks, malware signatures).  
- **Network:**  
  - Open inbound ports: `1514/udp` (agent communication), `55000/tcp` (Elasticsearch), `5601/tcp` (Kibana dashboard).  
  - Enable SSL/TLS for encrypted communication with agents.  

---

#### **3. Shuffle**  
**Hardware Requirements:**  
- **Host System:** Cloud-based VM (Ubuntu 22.04 LTS).  
- **CPU:** 2-core processor.  
- **RAM:** 4 GB minimum.  
- **Storage:** 20 GB disk space.  

**Software Configuration:**  
- **OS:** Ubuntu 22.04 LTS.  
- **Shuffle:** Docker-based deployment with latest stable image.  
- **Integrations:** Configure connectors for Wazuh Manager (API) and TheHive (webhook).  
- **Enrichment Workflows:**  
  - Automate IoC enrichment using free threat intelligence feeds (e.g., AbuseIPDB, VirusTotal API).  
  - Format alerts into TheHive-compatible JSON schema.  

---

#### **4. TheHive**  
**Hardware Requirements:**  
- **Host System:** Cloud-based VM (Ubuntu 22.04 LTS).  
- **CPU:** 4-core processor.  
- **RAM:** 8 GB minimum.  
- **Storage:** 50 GB disk space (for case management and evidence storage).  

**Software Configuration:**  
- **OS:** Ubuntu 22.04 LTS.  
- **TheHive:** Docker-based deployment with PostgreSQL database.  
- **Integrations:**  
  - Configure webhook to receive alerts from Shuffle.  
  - Enable Cortex for automated response actions (e.g., IP blocking, malware analysis).  
- **User Roles:** Define roles (Admin, Analyst, Viewer) with RBAC policies.  

---

#### **5. Network Architecture**  
**Requirements:**  
- **Internal Network (Home Lab):**  
  - Static IP assignment for Windows 10 PC running Wazuh Agent.  
  - Firewall rules to allow agent-to-manager communication.  
- **Cloud Environment:**  
  - Isolated VPC/VNet for Wazuh Manager, Shuffle, and TheHive.  
  - Security groups restricting access to Kibana (port `5601/tcp`) and TheHive UI (port `9000/tcp`) to authorized IPs only.  
- **VPN Setup (Optional):** Secure tunnel (WireGuard/OpenVPN) for remote SOC analyst access.  

---

#### **6. Security Configurations**  
- **SSL/TLS Certificates:** Deploy Let’s Encrypt certificates for all web interfaces (Kibana, TheHive).  
- **Authentication:**  
  - Kibana: Configure LDAP/Active Directory integration for SOC analysts.  
  - TheHive: Enable MFA for user logins.  
- **Data Encryption:** Encrypt Elasticsearch indices and PostgreSQL databases at rest.  

---

#### **7. Hardware/Software Summary Table**  
| **Component**       | **Hardware**                          | **Software**                                                                 |  
|----------------------|---------------------------------------|------------------------------------------------------------------------------|  
| **Wazuh Agent**      | Windows 10 PC, 4GB RAM, 50GB storage | Wazuh Agent v4.7, Windows Event Logs, Sysmon                                 |  
| **Wazuh Manager**    | 4-core VM, 8GB RAM, 100GB SSD        | Ubuntu 22.04, Wazuh Manager v4.7, Elastic Stack (v8.10)                      |  
| **Shuffle**          | 2-core VM, 4GB RAM, 20GB storage     | Ubuntu 22.04, Docker v24.0, Shuffle v1.1.1                                   |  
| **TheHive**          | 4-core VM, 8GB RAM, 50GB storage     | Ubuntu 22.04, Docker v24.0, TheHive v4.1, PostgreSQL v14                     |  

---

#### **8. Dependencies**  
- **Wazuh:** Elastic Stack (Elasticsearch, Logstash, Kibana).  
- **Shuffle:** Python 3.8+, Docker Compose.  
- **TheHive:** PostgreSQL, Cortex (for automated actions).  
- **APIs:** AbuseIPDB (free tier), VirusTotal (free/public API).  

---

This streamlined requirements document focuses exclusively on **hardware/software configurations** and **technical specifications** for a bachelor’s-level SOC automation project, omitting non-functional elements like testing, training, or community support.
