# Lab-Setup-and-Testing

## What I Did

* Upgraded desktop to Windows 11
* Installed VMware Workstation Pro
* Set up Metasploitable and Domain Controller VMs
* Changed networking from NAT to Bridged
* Removed Windows 10 from HP laptop
* Installed Kali Linux
* Updated both machines
* Documented every step

---

## Why It Matters

* You need a working lab to test tools like Nessus and Metasploit
* If the network doesn't connect, nothing else works
* Switching from NAT to Bridged solved remote access issues

Document and track all your IP addresses.
Set up port forwarding to allow RDP access.

---

## Port Forwarding in VMware

**Custom rules set:**

* Port `xxxxx` to Domain Controller
* Port `xxxxx` to Metasploitable

**From Kali:**

```bash
rdesktop <desktop_ip>:xxxxx
rdesktop <desktop_ip>:xxxxx
```

---

## RDP Fixes

* Enabled RDP on both VMs
* Set Security Layer to "RDP Security Layer"
* Allowed RDP through Windows Firewall

---

## Nessus Scan

* Ran Nessus from Kali
* Scanned the Metasploit VM
* Found MS17-010 (EternalBlue)

---

## Exploit and Keylogger

* Opened Metasploit on Kali
* Used `ms17_010_eternalblue` exploit
* Got a meterpreter shell
* Migrated to `explorer.exe`
* Started keylogger
* Typed “random message” in Notepad on Metasploit VM
* Dumped keystrokes in Kali

---

## What You Can Try

* Set up a lab like this
* Break the network
* Fix it
* Then try running a real exploit

Are you confident your setup can handle a real-world test?

---

## Next Steps

* Script the setup
* Add monitoring tools
* Test more exploits
