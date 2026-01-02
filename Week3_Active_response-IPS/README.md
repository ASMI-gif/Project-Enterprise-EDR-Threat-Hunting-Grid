# Week 3 – Active Response (IPS) using Wazuh

## Objective
The goal of Week 3 is to implement and validate **Intrusion Prevention System (IPS)** functionality using **Wazuh Active Response**.  
A simulated **SSH brute-force attack** is launched from an attacker machine, and Wazuh is configured to automatically block the attacker’s IP using a firewall rule on the target host.

---

## Environment Setup

| Component | Role | IP Address |
|---------|-----|-----------|
| Wazuh Manager | Detection & Response | 10.0.2.7 |
| Xubuntu | Wazuh Agent (Target) | 10.0.2.8 |
| Kali Linux | Attacker | 10.0.2.6 |

Network Mode: **NAT**

---

## Tools & Technologies Used
- Wazuh Manager & Agent
- SSH (OpenSSH)
- Hydra (Brute-force simulation)
- UFW / iptables
- Kali Linux
- Xubuntu Linux

---

## Step 1: SSH Service Validation on Target Host

The SSH service was verified and enabled on the Xubuntu agent machine to allow SSH-based attack simulation.

**Command:**
```bash
sudo systemctl status ssh

