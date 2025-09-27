# Metasploit-Meterpreter

## TryHackMe: Metasploit – Meterpreter Room  
**Status:** Completed  
**Badge Earned:** Metasploit  
**Tools Used:** Nmap, Metasploit Framework  
**Target:** 10.10.11.181 (Windows 7 SP1)

### 🔍 Reconnaissance
Executed a detailed Nmap scan using:
```bash
nmap -sV -sC --script vuln -oN blue.nmap 10.10.11.181
```
Discovered open SMB port (445) and confirmed vulnerability to **MS17-010 (EternalBlue)**.

### 💥 Exploitation
Used Metasploit to exploit the SMB vulnerability:
- Module: `exploit/windows/smb/ms17_010_eternalblue`
- Payload: `windows/x64/meterpreter/reverse_tcp`
- Result: Successful Meterpreter session

### 🧬 Post-Exploitation
Performed system enumeration and credential harvesting:
- `sysinfo`, `getuid`, `hashdump`, `screenshot`, `shell`
- Established persistence with `run persistence`

### 🛡️ Mitigation Recommendations
- Patch MS17-010 immediately
- Disable SMBv1
- Implement EDR and network segmentation

---

This room sharpened my red team skills and deepened my understanding of post-exploitation workflows using Meterpreter. It’s now part of my growing cybersecurity portfolio focused on offensive security and ethical hacking.
