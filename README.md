Detailed Report on Setting Up a Cybersecurity Environment with VirtualBox, Ubuntu Server, Docker, TheHive5, MISP, Cortex, Cassandra, Elasticsearch, and Wazuh
1. Install VirtualBox
Step-by-Step Instructions:
Download VirtualBox: Go to the VirtualBox website and download the appropriate version for your operating system.
Run the Installer: Open the downloaded file and follow the installation prompts.
Configure VirtualBox: After installation, launch VirtualBox and configure any global settings as needed.
2. Download Ubuntu Server 22.04 LTS Image and PuTTY
Step-by-Step Instructions:
Download Ubuntu Server 22.04 LTS:
Visit the Ubuntu website and download the Ubuntu Server 22.04 LTS ISO file.
Download PuTTY:
Visit the PuTTY website and download the appropriate version for your operating system.
3. Install Ubuntu Server with +8GB RAM and +4 Processors
Step-by-Step Instructions:
Create a New Virtual Machine:
Open VirtualBox and click on New.
Name your VM and choose Linux and Ubuntu (64-bit).
Allocate at least 8GB of RAM and 4 processors.
Attach the ISO File:
Go to Settings > Storage and attach the downloaded Ubuntu ISO file to the virtual CD/DVD drive.
Start the VM:
Start the VM and follow the installation prompts to install Ubuntu Server.
Allocate sufficient disk space (at least 20GB recommended).
Complete the installation by setting up the initial user and network configuration.
4. Download Docker.io and Docker Compose in Ubuntu
Step-by-Step Instructions:
Update Package Index:
bash
Copy code
sudo apt update
Install Docker:
bash
Copy code
sudo apt install docker.io
Install Docker Compose:
bash
Copy code
sudo apt install docker-compose
Start and Enable Docker:
bash
Copy code
sudo systemctl start docker
sudo systemctl enable docker
5. Install Docker Images of TheHive5, MISP, Cortex, Cassandra, Elasticsearch
Step-by-Step Instructions:
Pull the Docker Images:
bash
Copy code
sudo docker pull thehiveproject/thehive:5
sudo docker pull misp/misp
sudo docker pull thehiveproject/cortex:3
sudo docker pull cassandra:latest
sudo docker pull elasticsearch:7.10.2
Run the Docker Containers:
bash
Copy code
sudo docker run -d --name cassandra cassandra:latest
sudo docker run -d --name elasticsearch -e "discovery.type=single-node" elasticsearch:7.10.2
sudo docker run -d --name thehive -p 9000:9000 thehiveproject/thehive:5
sudo docker run -d --name misp -p 443:443 misp/misp
sudo docker run -d --name cortex -p 9001:9001 thehiveproject/cortex:3
6. Install Wazuh
Two Methods:
Method 1: Using OVA File
Download Wazuh OVA:
Visit the Wazuh website and download the OVA file.
Import OVA into VirtualBox:
Open VirtualBox and go to File > Import Appliance.
Select the downloaded OVA file and follow the prompts to import it.
Method 2: Install via Command Line
Run Wazuh Installation Script:
bash
Copy code
curl -sO https://packages.wazuh.com/4.3/wazuh-install.sh
sudo bash wazuh-install.sh -a
7. Configure Required Files Using PuTTY by SSH into the Server
Step-by-Step Instructions:
SSH into the Ubuntu Server:
Open PuTTY and enter the IP address of the Ubuntu server.
Login with your Ubuntu server credentials.
Edit Configuration Files:
Use a text editor like nano or vim to edit configuration files as needed.
bash
Copy code
sudo nano /path/to/config/file.yml
8. Access the Dashboards on Localhost
Access URLs:
TheHive: http://localhost:9000
MISP: https://localhost
Cortex: http://localhost:9001
Wazuh: http://localhost:5601 (assuming Kibana is used)
9. Create Users, Admins, Organization, and API Keys
Step-by-Step Instructions:
TheHive:
Access http://localhost:9000
Navigate to the admin panel and create users and organizations.
Generate API keys in the user settings.
Cortex:
Access http://localhost:9001
Create users and generate API keys.
MISP:
Access https://localhost
Create users, organizations, and generate API keys under the administration section.
10. Integrate API Keys by Configuring YAML Files
Step-by-Step Instructions:
Edit TheHive Configuration:
bash
Copy code
sudo nano /etc/thehive/application.conf
Add the API keys and other configuration details.
Edit Cortex Configuration:
bash
Copy code
sudo nano /etc/cortex/application.conf
Add the API keys and other necessary details.
Edit MISP Configuration:
bash
Copy code
sudo nano /var/www/MISP/app/Config/config.php
Insert the API keys and other relevant configurations.
11. Install Wazuh Agent on Client
Step-by-Step Instructions:
Download and Install Agent:
Follow the instructions on the Wazuh website to download and install the agent on the client machine.
bash
Copy code
sudo apt install wazuh-agent
Configure the Agent:
Edit the agent configuration file to point to the Wazuh manager.
bash
Copy code
sudo nano /var/ossec/etc/ossec.conf
12. Generate Agent in Wazuh Manager
Step-by-Step Instructions:
Register the Agent:
bash
Copy code
sudo /var/ossec/bin/manage_agents
Follow the prompts to add a new agent.
Start the Agent and Manager:
bash
Copy code
sudo systemctl start wazuh-agent
sudo systemctl start wazuh-manager
13. View Wazuh Logs in TheHive5
Step-by-Step Instructions:
Integrate Wazuh with TheHive5:
Ensure Wazuh is configured to send alerts to TheHive.
Check TheHive dashboard for incoming logs and alerts from Wazuh.
14. Create Rules in Wazuh
Step-by-Step Instructions:
Edit Local Rules File:
bash
Copy code
sudo nano /var/ossec/etc/rules/local_rules.xml
Add Custom Rules:
Add rules with IDs greater than 100000.
xml
Copy code
<group name="custom_rules">
  <rule id="100001" level="3">
    <decoded_as>json</decoded_as>
    <description>Custom rule description</description>
    <options>
      <!-- Define rule options here -->
    </options>
  </rule>
</group>
Restart Wazuh Manager:
bash
Copy code
sudo systemctl restart wazuh-manager
By following these steps, you will have a fully functional cybersecurity environment with TheHive5, MISP, Cortex, Cassandra, Elasticsearch, and Wazuh, integrated and ready for use.
