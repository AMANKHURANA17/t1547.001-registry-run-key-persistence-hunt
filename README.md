# t1547.001-registry-run-key-persistence-hunt

## Overview

This project documents a threat hunting and detection engineering exercise focused on identifying Windows persistence techniques associated with **MITRE ATT&CK T1547.001 -> Registry Run Keys / Startup Folder**.

The objective was to develop behavioral hypotheses, validate them against endpoint telemetry, and translate the resulting detection logic into portable Sigma rules.

The detections cover multiple techniques an attacker may use to establish persistence through Registry Run Keys, Startup Folders, PowerShell, `reg.exe`, WMI `StdRegProv`, and DLL execution through `rundll32.exe`.

---

## Objectives

- Develop threat hunting hypotheses based on attacker persistence behaviors.
- Identify relevant endpoint telemetry and detection opportunities.
- Validate hypotheses using telemetry.
- Translate validated hunting logic into Sigma detection rules.
- Map detections to relevant MITRE ATT&CK techniques.
- Document false positives and environment-specific tuning considerations.
- Build portable detections that can be adapted to other SIEM/EDR platforms.

---

## Attack Technique

| Technique | ATT&CK ID | Description |
|---|---|---|
| Registry Run Keys / Startup Folder | T1547.001 | Adversaries may establish persistence by configuring Registry Run Keys or Startup Folders to execute malicious payloads during system or user startup. |

---

## Detection Hypotheses

### 1. Add malicious script-based files or command interpreters to Registry Run Keys

- Add malicious `.bat`, `.cmd`, `.ps1`, `.js`, `.vbs`, `.py`, or similar script-based files to Run/RunOnce keys.
- Configure command-line interpreters such as PowerShell, WScript, CScript, MSHTA, Python, Perl, or Ruby to execute during startup.

### 2. Add malicious files or payloads to Windows Startup Folders

- Place malicious executables, scripts, shortcuts, or other payloads in Windows Startup Folders.
- Configure malicious or unsigned processes to execute automatically when a user logs on.

### 3. Use `reg.exe` to modify Registry Run Keys

- Use `reg.exe add` to create or modify Run or RunOnce registry keys for persistence.
- Configure registry values with commands or payloads that execute during user logon.

### 4. Use PowerShell or .NET-based scripts to modify Registry Run Keys

- Use PowerShell cmdlets such as `Set-ItemProperty` or `New-ItemProperty` to create or modify Registry Run/RunOnce keys.
- Use .NET-based registry manipulation to establish persistence through existing or newly created Run Keys.

### 5. Use WMI `StdRegProv` to modify Registry Run Keys

- Use PowerShell and WMI `StdRegProv` to create or modify Registry Run/RunOnce keys for persistence.

### 6. Add malicious DLLs to Registry Run Keys

- Configure Registry Run/RunOnce keys to execute DLL payloads using `rundll32.exe`.
- Abuse DLL execution through Registry Run Keys to establish persistence.

---

## Methodology

The detection development process followed the following workflow:

```text
Threat Behavior
      ↓
Detection Hypothesis
      ↓
Telemetry Identification
      ↓
Hunting Query
      ↓
Result Validation
      ↓
Detection Logic Refinement
      ↓
Sigma Rule
      ↓
False Positive Analysis
      ↓
Production Validation
