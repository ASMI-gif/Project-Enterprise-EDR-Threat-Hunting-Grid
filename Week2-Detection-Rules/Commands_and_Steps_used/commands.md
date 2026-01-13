# Week 2 – Commands and Implementation Steps

This document contains all commands and configuration steps used during **Week 2 – Detection Rules (The Logic)**.  
The tasks were implemented using **Wazuh SIEM** with both **Linux and Windows agents**.

---

## 1. File Integrity Monitoring (FIM) Configuration

### 1.1 Linux Agent – FIM Setup

#### Edit Agent Configuration
```bash
sudo nano /var/ossec/etc/ossec.conf

```
---

#### Add FIM Configuration

```bash
<syscheck>
  <directories check_all="yes" realtime="yes">/opt/sensitive_app</directories>
</syscheck>

```
---

#### Restart Wazuh-agent

```bash

sudo systemctl restart wazuh-agent

```

---

#### Gate Check – Manual File Modification
```bash

sudo nano /opt/myapp/logs/app_error.log

```
---
#### or 
```bash

echo 'APPFAIL: user=test code=401 reason="wrong"' | sudo tee -a /opt/myapp/logs/app_error.log

```
---

### Windows Agent -FIM Setup

#### Edit Agent Configuration

```powershell

notepad "C:\Program Files (x86)\ossec-agent\ossec.conf"

```
---

#### Add FIM Directory 

```bash 

<syscheck>
  <directories check_all="yes" realtime="yes">C:\Windows\System32</directories>
</syscheck>
 
#### Restart Wazuh agent Service 

```powershell

Restart-Service -Name Wazuh
 ```
---

####  Create a harmless test file

##### Open PowerShell as Administrator:

```powershell

New-Item -Path "C:\Windows\System32\fim-test.txt" -ItemType File

```
---


##### Modify the file to trigger FIM
```powershell

Add-Content -Path "C:\Windows\System32\fim-test.txt" -Value "Test modification at $(Get-Date)"

```
---

##### This will generate a file modification event in the Wazuh

### 2. Custom XML Decoder Configuration

#### Linux – Custom Decoder Setup

##### Edit Local Decoder File 

```bash 

sudo nano /var/ossec/etc/decoders/local_decoders_myapp.xml

```
---
##### Custom Decoder Example


```bash

<decoder name="myapp_first">
  <prematch>APPFAIL:</prematch>
  <regex>APPFAIL:user=([^ ]+)\scode=([0-9]+)\sreason="(.+)"</regex>
  <order>user</order>
  <order>code</order>
  <order>reason</order>
</decoder>

```
---

#### Windows – Proprietary Log File Path Example
##### Custom application logs monitored from:

```text

C:\ProgramData\CustomApp\logs\app.log

```
---
##### Log entries forwarded to Wazuh agent and parsed using the same decoder logic.
##### Custom Detection Rules
##### Edit Local Rules File (Manager)
```bash 

sudo nano /var/ossec/etc/rules/local_rules.xml

```
---
##### High-Severity Rule Example
```bash 

<rule id="100210" level="12">
  <if_matched_sid>custom_app_log</if_matched_sid>
  <description>High severity event detected in proprietary application log</description>
  <mitre>T1059</mitre>
</rule>

```
---
##### Restart Wazuh Manager
```bash

sudo systemctl restart wazuh-manager

```
---
#### Vulnerability Detector Configuration
##### Enable Vulnerability Detection (Manager)
##### Edit Configuration File
```bash 

sudo nano /var/ossec/etc/ossec.conf

```
---

##### Enable Module

```bash 

<vulnerability-detection>
  <enabled>yes</enabled>
</vulnerability-detection>

```
---
```bash 

sudo systemctl restart wazuh-manager

```
---

##### Linux Agent – Vulnerability Scan Validation
```bash 

sudo systemctl restart wazuh-agent

```
---

Confirmed CVE data visible in Wazuh dashboard under Vulnerability Detection.
##### Windows Agent – Vulnerability Scan Validation

```powershell

Restart-Service -Name Wazuh

```
---

Verified Windows OS and installed software vulnerabilities displayed in dashboard.
#### Alert Verification and Validation

-File modifications detected in real time

-Custom decoder logs parsed correctly

-High-severity alerts generated

-Alerts visible in dashboard within 5 seconds

-Vulnerability data successfully ingested from agents

#### Outcome

✅ FIM correctly configured for Linux and Windows agents

✅ Custom decoders and rules functioning as expected

✅ Vulnerability detection enabled and validated

✅ Gate check passed successfully
