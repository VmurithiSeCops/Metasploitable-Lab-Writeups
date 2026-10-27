# Lab Exercise: Target Enumeration & Assessment

## 1. Environment Details
* **Target IP:** `192.168.0.120` (Metasploitable Lab VM)
* **Host Operating System:** Linux / Ubuntu (Metasploitable v2)
* **Objective:** Perform initial host discovery, identify open ports, and document vulnerable services.

---

## 2. Reconnaissance & Host Discovery
Initial ping sweep confirmed target availability on the local subnet:
```bash
nmap -sn 192.168.0.120 
```
## 3. Full Port & Service Scan
Executed an exhaustive TCP SYN scan with version detection to map running services:
```bash
nmap -p- -sS -sV -O 192.168.0.120 -oA lab_target_scan
```
### Key Findings Summary
* **Port 21/tcp (FTP):** vsftpd 2.3.4 (Known backdoor vulnerability vector)
* **Port 22/tcp (SSH):** OpenSSH 4.7p1
* **Port 80/tcp (HTTP):** Apache/2.2.8 running vulnerable web applications (DVWA, Mutillidae)
* **Port 445/tcp (SMB):** Samba 3.0.20

## 4. Analysis & Triage Recommendations
1. **Patching & Updates:** Outdated software versions (such as vsftpd 2.3.4 and Samba 3.0.20) must be upgraded to secure, vendor-supported releases.
2. **Access Control:** Restrict administrative shell access and disable anonymous FTP login capabilities across production segments.
