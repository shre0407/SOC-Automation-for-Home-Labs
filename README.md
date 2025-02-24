markdown
Copy
# SOC Home Automation Project

📌 **Overview**

This repository provides a detailed guide to setting up a **Cybersecurity Operations Center (SOC) Home Automation Project** using the following tools:
- VirtualBox
- Ubuntu Server
- Docker
- TheHive5
- MISP
- Cortex
- Cassandra
- Elasticsearch
- Wazuh

---

## 🎥 **Need Help?**

If you get stuck (and you will!), refer to this **YouTube playlist** for step-by-step video tutorials:  
[YouTube Playlist](https://www.youtube.com/playlist-link-here)

---

## 🏗️ **Setup Guide**

### 1️⃣ **Install VirtualBox**
1. Download VirtualBox from the [official website](https://www.virtualbox.org/).
2. Run the installer and follow the prompts.
3. Launch VirtualBox and configure global settings.

---

### 2️⃣ **Download Ubuntu Server 22.04 LTS and PuTTY**
- **Ubuntu Server 22.04 LTS**: [Download here](https://ubuntu.com/download/server)
- **PuTTY**: [Download here](https://www.putty.org/)

---

### 3️⃣ **Install Ubuntu Server (VM Configuration)**
1. Create a new VM in VirtualBox.
2. Allocate at least **8GB RAM** and **4 processors**.
3. Attach the Ubuntu ISO and install it.
4. Allocate at least **20GB disk space**.

---

### 4️⃣ **Install Docker and Docker Compose**
Run the following commands:
```bash
sudo apt update
sudo apt install docker.io
sudo apt install docker-compose
sudo systemctl start docker
sudo systemctl enable docker
5️⃣ Install Docker Images
Pull the required Docker images:

bash
Copy
sudo docker pull thehiveproject/thehive:5
sudo docker pull misp/misp
sudo docker pull thehiveproject/cortex:3
sudo docker pull cassandra:latest
sudo docker pull elasticsearch:7.10.2
Run the containers:

bash
Copy
sudo docker run -d --name cassandra cassandra:latest
sudo docker run -d --name elasticsearch -e "discovery.type=single-node" elasticsearch:7.10.2
sudo docker run -d --name thehive -p 9000:9000 thehiveproject/thehive:5
sudo docker run -d --name misp -p 443:443 misp/misp
sudo docker run -d --name cortex -p 9001:9001 thehiveproject/cortex:3
6️⃣ Install Wazuh
Method 1: Using OVA File
Download the Wazuh OVA file and import it into VirtualBox.

Method 2: Install via Command Line
bash
Copy
curl -sO https://packages.wazuh.com/4.3/wazuh-install.sh
sudo bash wazuh-install.sh -a
7️⃣ Configure Required Files via SSH
bash
Copy
ssh user@your-server-ip
sudo nano /path/to/config/file.yml
8️⃣ Access Dashboards on Localhost
TheHive: http://localhost:9000

MISP: https://localhost

Cortex: http://localhost:9001

Wazuh: http://localhost:5601 (with Kibana)

9️⃣ Create Users, Admins, Organizations, and API Keys
TheHive: Navigate to the admin panel to create users & API keys.

Cortex: Configure users and generate API keys.

MISP: Set up organizations, users, and API keys.

🔟 Integrate API Keys
Edit the configuration files:

bash
Copy
sudo nano /etc/thehive/application.conf  # TheHive
sudo nano /etc/cortex/application.conf   # Cortex
sudo nano /var/www/MISP/app/Config/config.php  # MISP
1️⃣1️⃣ Install Wazuh Agent on Client
bash
Copy
sudo apt install wazuh-agent
sudo nano /var/ossec/etc/ossec.conf
1️⃣2️⃣ Generate Agent in Wazuh Manager
bash
Copy
sudo /var/ossec/bin/manage_agents
sudo systemctl start wazuh-agent
sudo systemctl start wazuh-manager
1️⃣3️⃣ View Wazuh Logs in TheHive5
Ensure Wazuh is configured to send alerts to TheHive.

1️⃣4️⃣ Create Rules in Wazuh
Edit the rules file:

bash
Copy
sudo nano /var/ossec/etc/rules/local_rules.xml
Add rules with IDs greater than 100000.
Restart Wazuh Manager:

bash
Copy
sudo systemctl restart wazuh-manager
✅ Summary
By following this guide, you'll have a fully functional SOC Home Automation environment integrated with:

TheHive5

MISP

Cortex

Cassandra

Elasticsearch

Wazuh

🚀 Happy Securing!

Copy

### Key Improvements:
1. **Formatting**: Used headers (`#`, `##`, `###`) for better structure.
2. **Code Blocks**: Wrapped commands in triple backticks (```) for readability.
3. **Links**: Added placeholder links for the YouTube playlist and downloads.
4. **Emojis**: Used emojis to make sections visually distinct and engaging.
5. **Consistency**: Ensured consistent formatting for commands, file paths, and URLs.

Feel free to replace the placeholder links with actual URLs and customize the content further as needed!
