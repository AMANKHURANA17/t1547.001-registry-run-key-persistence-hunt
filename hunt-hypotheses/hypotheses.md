## Hypothesis/Narrative Statement

An attacker may establish persistence by abusing Windows Registry Run Keys, Startup Folders, and related registry modification mechanisms to execute malicious payloads during system or user startup.

The attacker may:

1. **Add malicious script-based files or command interpreters to Registry Run Keys**
   - Add malicious `.bat`, `.cmd`, `.ps1`, `.js`, `.vbs`, `.py`, or similar script-based files to Run/RunOnce keys.
   - Configure command-line interpreters such as PowerShell, WScript, CScript, MSHTA, Python, Perl, or Ruby to execute during startup

2. **Add malicious files or payloads to Windows Startup Folders**
   - Place malicious executables, scripts, shortcuts, or other payloads in Windows Startup Folders.
   - Configure malicious or unsigned processes to execute automatically when a user logs on.

3. **Use `reg.exe` to modify Registry Run Keys**
   - Use `reg.exe add` to create or modify `Run` or `RunOnce` registry keys for persistence.
   - Configure the registry value with a `REG_SZ` command or payload that executes during user logon.

4. **Use PowerShell or .NET-based scripts to modify Registry Run Keys**
   - Use PowerShell cmdlets such as `Set-ItemProperty` or `New-ItemProperty` to create or modify Registry Run/RunOnce keys.
   - Use .NET-based registry manipulation to establish persistence through existing or newly created Run Keys.

5. **Use WMI StdRegProv to modify Registry Run Keys**
   - Use PowerShell and WMI `StdRegProv` to create or modify Registry Run/RunOnce keys for persistence.

6. **Add malicious DLLs to Registry Run Keys**
   - Configure Registry Run/RunOnce keys to execute DLL payloads using `rundll32.exe`.
   - Abuse DLL execution through Registry Run Keys to establish persistence.


