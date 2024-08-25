# Azure-Honeypot-Lab

## Using Microsoft Sentinel To Monitor A Honeypot & Map Live Attacks

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

***

### TL;DR

_**Technologies used**: Virtual Machines, Azure Log Analytics Workspace, Azure Sentinel (SIEM), PowerShell, Kusto Query Language (KQL), Geolocation API_

In this lab, I set up a vulnerable virtual machine and exposed it to the public internet as a honeypot. I then configured Azure’s Log Analytics Workspace to collect logs from failed remote login attempts. Lastly, I used Azure Sentinel to analyze the logs and created a heatmap that visualized the geographic locations of the attackers on a world map.

<figure><img src=".gitbook/assets/Screenshot 2024-08-13 091539 (1).png" alt=""><figcaption><p>Project Overview</p></figcaption></figure>

***

### Table Of Contents

* Step 1: Set Up the Honeypot
* Step 2: Configure Data Collection in Azure Sentinel
* Step 3: Set Up Custom Logs for Failed Login Attempts
* Step 4: Analyze and Process Logs in Azure Sentinel
* Step 5: Visualize Attacks on a Map

***

### Set Up the Honeypot

**Create a Virtual Machine (VM):** Deploy a vulnerable VM on Azure. Use a minimal security configuration to make it appealing to attackers.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

**Expose the VM to the Internet:** Assign a public IP address to the VM, open common ports (e.g., RDP, SSH), and reduce security settings.

<figure><img src=".gitbook/assets/Screenshot 2024-08-13 095331.png" alt=""><figcaption></figcaption></figure>

***

### Configure Data Collection in Azure Sentinel

**Enable Azure Sentinel:** Go to the Azure portal, create a Log Analytics workspace, and enable Azure Sentinel.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Connect Data Sources:** Integrate data sources like Azure Security Center, Azure Firewall, and the VM’s diagnostic logs with Azure Sentinel.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

***

### Set Up Custom Logs for Failed Login Attempts

**Create a Custom Log:** Use a custom log in Log Analytics Workspace to collect specific event IDs related to failed login attempts (e.g., Event ID 4625 for RDP).

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**Ingest Logs:** Write a script or use built-in tools to ingest logs from your honeypot into Azure Log Analytics.

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

***

### Visualize Attacks on a Map

**Create a Workbook:** Use Sentinel’s workbook feature to create a custom dashboard that includes a world map visualization.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

**Plot Attacker Locations:** Use the geographic data from the logs to plot the locations of attack sources on the map.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

**Monitor in Real-Time:** Continuously monitor the map to see live attacks and trends over time.

***

### Takeaways

Before completing the lab, I noticed a surge of brute-force attempts within just two hours of deploying the honeypot, thanks to the locally running PowerShell script. This experience reinforced how quickly vulnerable systems are discovered on the internet. A key takeaway is to avoid common usernames like "administrator," "admin," "user," "guest," and "PC," which were frequently targeted during these attacks. Using these usernames could have significantly increased the risk of a breach.

**Room for Improvement:**\
PowerShell was a quick solution for exporting security logs, but it’s not ideal for extensive log collection. A tool like Splunk could have provided a more efficient and scalable approach.

**Tip of the Iceberg:**\
The heatmap focused solely on failed RDP login attempts, but Azure cloud VMs have other services like SMB open by default, which could be targeted for brute-force attacks. I limited log collection to avoid exhausting IP geolocation API requests, but it’s clear that the system was likely being targeted on multiple fronts.

**Technical Skills Learned:**

* **Microsoft Azure Cloud:** I was new to Azure, but this lab taught me how to integrate its services to achieve a specific goal.
* **PowerShell:** With limited prior experience, I learned to use PowerShell for local system log analysis.
* **Kusto Query Language (KQL):** My first experience with KQL was challenging but rewarding, as I learned to clean and analyze log data in Azure.

\
