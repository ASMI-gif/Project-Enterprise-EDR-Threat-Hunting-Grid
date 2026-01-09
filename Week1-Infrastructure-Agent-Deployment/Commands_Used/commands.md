## Week 1 – Wazuh Agent Manual Installation Commands

---

### Agent Installation (Ubuntu/Linux)

### Update system packages

```bash
sudo apt update && sudo apt upgrade -y

```
---
## Install curl(if not installed)

```bash

sudo apt install curl -y

```
---
## Download Wazuh Agent package

```bash
curl -sO https://packages.wazuh.com/4.14/wazuh-agent_4.14.0-1_amd64.deb

```
---

## Install Wazuh Agent

```bash 

sudo dpkg -i wazuh-agent_4.14.0-1_amd64.deb

```
---

## Fix dependency issues (if any)

```bash

sudo apt --fix-broken install -y

```
---
## Configure Wazuh Manager IP

```bash 

sudo nano /var/ossec/etc/ossec.conf

```
---

```bash

<client>
  <server>
    <address>WAZUH_MANAGER_IP</address>
    <port>1514</port>
    <protocol>tcp</protocol>
  </server>
</client>

```
---


## Enable and Start the agent

```bash 

  GNU nano 8.7                                 commands-used                                 Modified
## Download Wazuh Agent package

```bash
curl -sO https://packages.wazuh.com/4.14/wazuh-agent_4.14.0-1_amd64.deb

```
---

## Install Wazuh Agent

```bash

sudo dpkg -i wazuh-agent_4.14.0-1_amd64.deb

```
---

## Fix dependency issues (if any)

```bash

sudo apt --fix-broken install -y

```
---
## Configure Wazuh Manager IP

```bash

sudo nano /var/ossec/etc/ossec.conf

```
---

```bash

<client>
  <server>
    <address>WAZUH_MANAGER_IP</address>
    <port>1514</port>
    <protocol>tcp</protocol>
  </server>
</client>

```
---


## Enable and Start the agent

```bash

sudo systemctl daemon-reexec
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

```
---
## Verify agent status

```bash 

sudo systemctl status wazuh-agent

```
---
 ## View agent logs

```bash 
 sudo tail -f /var/ossec/logs/ossec.log

```
---

## 🪟 Windows Server 2022 – Wazuh Agent Installation (Manual)

---

### Step 1: Download Wazuh Agent Installer
# Download the official Wazuh agent MSI for Windows
https://packages.wazuh.com/4.14/windows/wazuh-agent-4.14.0-1.msi

---

### Step 2: Install Wazuh Agent (GUI Method)
# Double-click the MSI file
# Click Next → Accept License → Next
# Enter the Wazuh Manager IP address
# Set a meaningful agent name (example: windows-server-2022)
# Complete the installation

---

### Step 3: Install Wazuh Agent (Command Line Method – Recommended)

# Open PowerShell as Administrator and run:
```powershell
msiexec /i wazuh-agent-4.14.0-1.msi /qn `
WAZUH_MANAGER="WAZUH_MANAGER_IP" `
WAZUH_AGENT_NAME="windows-server-2022"

```
---
### Step 4: Start Wazuh Agent Service
 ```powershell
net start WazuhSvc

```
---
### Step 5: Verify Wazuh Agent Status
```powershell

sc query WazuhSvc

```
---

### Step 6: Verify Agent Logs

```powershell

C:\Program Files (x86)\ossec-agent\ossec.log

```
---
### Step 7: Confirm Agent in Wazuh Dashboard

#Login to Wazuh Dashboard
#Navigate to:
#Management → Agents
#Verify agent status is "Active"
---
