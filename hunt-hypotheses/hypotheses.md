## Hypothesis/Narrative Statement

An attacker may establish persistence by abusing Windows Registry Run Keys, Startup Folders, and related registry modification mechanisms to execute malicious payloads during system or user startup.

The attacker may:

1. **Add malicious script-based files or command interpreters to Registry Run Keys**
   - Add malicious `.bat`, `.cmd`, `.ps1`, `.js`, `.vbs`, `.py`, or similar script-based files to Run/RunOnce keys.
   - Configure command-line interpreters such as PowerShell, WScript, CScript, MSHTA, Python, Perl, or Ruby to execute during startup

2. **Add malicious files or payloads to Windows Startup Folders**
   - Place malicious executables, scripts, shortcuts, or other payloads in Windows Startup Folders.
   - Configure malicious or unsigned processes to execute automatically when a user logs on.

