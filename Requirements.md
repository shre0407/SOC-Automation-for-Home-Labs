Wazuh Agent:
The Wazuh Agent serves as the foundational component of the SOC automation project, residing on a Windows 10 PC within the home lab environment. Its primary function is to collect security-related events and logs from the host system and forward them to the central management server, the Wazuh Manager, for further analysis.
 
Wazuh Manager:
Installed on a cloud-based server, the Wazuh Manager acts as the nerve center of the SOC automation project. It receives, processes, and analyzes the security events and logs forwarded by the Wazuh Agent, correlating them to generate alerts based on predefined rules and policies. Additionally, the Wazuh Manager provides centralized management and configuration capabilities for the entire Wazuh infrastructure.
Shuffle:
Shuffle serves as an intermediary component in the SOC automation workflow, receiving alerts from the Wazuh Manager and enriching them with additional context before forwarding them to TheHive for further analysis and response orchestration. This enrichment process involves augmenting alerts with Indicators of Compromise (IoCs) and other relevant information to enhance their relevance and actionable insights.
TheHive:
Operating within the cloud environment alongside Shuffle, TheHive serves as the incident response and case management platform for the SOC automation project. It receives enriched alerts from Shuffle, aggregates them into actionable cases, and facilitates collaboration among SOC analysts through its intuitive user interface. Additionally, TheHive initiates response actions based on analyst decisions, orchestrating mitigation efforts to address detected security threats effectively.
