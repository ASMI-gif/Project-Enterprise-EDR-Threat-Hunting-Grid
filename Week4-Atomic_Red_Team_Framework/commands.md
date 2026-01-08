# Week 4 – Atomic Red Team | Commands Used (Windows Agent)

This document lists the commands executed on a Windows endpoint to simulate adversary behavior using the Atomic Red Team framework and to validate EDR detection and response capabilities.

---

## Environment Details

- Operating System: Windows Server 2022
- Agent Type: Windows Wazuh Agent
- Execution Context: Administrator
- Framework: Atomic Red Team
- MITRE ATT&CK Technique: T1490 – Inhibit System Recovery
- Objective: Simulate ransomware-style behavior and observe detections

---

## 1. Open PowerShell with Administrative Privileges

```powershell
Start-Process powershell -Verb RunAs

```
---

## 2. Temporarily Allow Script Execution

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force

```
---

## 3.Download and Install Atomic Red Team 

```powershell
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1')

```
---

## 4. Import Atomic Red Team Module
```powershell
Import-Module "C:\AtomicRedTeam\invoke-atomicredteam\Invoke-AtomicRedTeam.psd1"

```
---

## 5.Verify Atomic Red Team Installation

```powershell
Get-Command Invoke-AtomicTest

```
---

## 6. List Atomic Tests for Technique T1490

```powershell
Invoke-AtomicTest T1490 -ShowDetails

```
---

## 7. Execute Atomic Test – Shadow Copy Deletion

```powershell
Invoke-AtomicTest T1490 -TestNumbers 1

```
---
## 8. Manual Shadow Copy Deletion (Ransomware Simulation)

```powershell
vssadmin delete shadows /all /quiet

```
---
## 9. Verify Shadow Copies Have Been Deleted

```powershell
vssadmin list shadows

```
## 10. Detection Validation

EDR generated alert for shadow copy deletion

Alert mapped to MITRE ATT&CK technique T1490

Kill Chain stage identified as Impact

Event correlation visible in SIEM (Kibana / OpenSearch)

## 11.Restore Powershell Execution Policy

```powershell
Set-ExecutionPolicy Restricted -Scope LocalMachine -Force

```
---

## Outcome

Successfully simulated ransomware-style behavior

EDR detection and response validated

Kill Chain visualization confirmed

---

