# Week 2: Detection Rules & Logic Implementation

## 🎯 Objective
The goal of Week 2 was to implement and validate **detection logic** inside the Wazuh SIEM by enabling security modules, creating custom rules, and verifying alert generation in near real time.

---

## 🔍 Scope of Work
- File Integrity Monitoring (FIM)
- Custom decoders and detection rules
- Vulnerability detection
- Alert validation and response time testing

---

## 🛠️ Configuration & Implementation

### 1️⃣ File Integrity Monitoring (FIM)
- Enabled FIM on critical system directories
- Monitored configuration files for unauthorized changes
- Generated alerts for file creation, modification, and deletion

**Monitored Paths:**
- `/etc/`
- `/var/www/`
- `C:\Windows\System32\`

---

### 2️⃣ Custom Decoders
- Created XML decoders to parse proprietary and uncommon log formats
- Extracted key fields such as:
  - Source IP
  - Username
  - Process name
  - Event type

**Purpose:**  
Improve visibility into logs not natively supported by default Wazuh rules.

---

### 3️⃣ Custom Detection Rules
- Implemented custom rules mapped to:
  - Suspicious file changes
  - Unauthorized access attempts
  - Privilege escalation indica
---
⬅️ **[Back to Weekly Breakdown](../README.md#-Weekly-Breakdown)**
