# Simulated Wireshark Packet Dissection Log
**Target Event:** Suspicious Port Scan & Unencrypted Credential Exfiltration

### Frame 104: Network Reconnaissance (SYN Scan)
- **Source IP:** 192.168.1.105 (Attacker)
- **Destination IP:** 192.168.1.20 (Target Web Server)
- **Protocol:** TCP
- **Flags:** 0x002 (SYN)
- **Destination Port:** 80, 443, 22, 3389 (Rapid sequence)
- **Analyst Note:** High-frequency TCP SYN packets sent to multiple consecutive ports within a 2-second window indicates an active Nmap stealth scan.

### Frame 412: Cleartext Authentication Exfiltration
- **Source IP:** 192.168.1.105
- **Destination IP:** 192.168.1.20
- **Protocol:** HTTP (TCP Port 80)
- **Request Method:** POST /login.php HTTP/1.1
- **Payload Hex / ASCII:**
  `Form item: "uname" = "admin"`
  `Form item: "passwd" = "Password123!"`
- **Analyst Note:** The adversary successfully intercepted or transmitted administrative credentials over an unencrypted layer-7 transit protocol (HTTP).
