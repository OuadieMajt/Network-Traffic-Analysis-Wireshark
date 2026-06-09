 # Network Traffic Analysis & Intrusion Detection via Wireshark
### Security Analyst Technical Case Study (Google Cybersecurity Certificate Project)

## 📌 Incident Objective
The objective of this analysis was to investigate a simulated corporate network anomaly flagged by an internal IDS alert. The objective was to isolate malicious packet captures (PCAPs), analyze the TCP three-way handshake sequence for anomalies, detect unauthorized port scanning, and intercept cleartext credential exploitation across network boundaries.

## 🛠️ Security Tools & Filters Utilized
- **Analysis Platform:** Wireshark Packet Analyzer
- **Target Protocols:** TCP, UDP, HTTP, DNS, ARP
- **Core Display Filters Mastered:**
  * `tcp.flags.syn == 1 and tcp.flags.ack == 0` (Isolates initial connection requests/SYN scans)
  * `http.request.method == "POST"` (Targets web-server form submissions and data exfiltration)
  * `ip.addr == 192.168.1.105` (Isolates all ingress/egress telemetry from the suspected rogue asset)

---

## 💻 Technical Investigation Walkthrough

### Phase 1: Identifying Network Reconnaissance
- Deployed advanced Wireshark display filters to track a spike in transmission anomalies.
- Observed a high volume of sequential TCP SYN packets targeting standard enterprise listening ports (22, 80, 443, 3389) on the internal domain subnet.
- **Analysis:** The absence of corresponding ACK packets from the target machine confirmed a malicious TCP half-open/stealth port scan (MITRE ATT&CK T1595.002).

### Phase 2: Dissecting Protocol Anomaly & Packet Payloads
- Isolated a localized transition from unencrypted HTTP traffic following the reconnaissance phase.
- Utilized Wireshark's **"Follow TCP Stream"** feature to reconstruct the layer-7 communication sequence between the external threat node and the internal asset.
- Successfully intercepted a plaintext `POST` request containing unencrypted configuration commands and compromised administrative credentials.

### Phase 3: Mitigation & Intrusion Defense Strategy
- Extracted the malicious MAC address and source IP vector from the Ethernet/IP frame headers.
- Formulated an immediate incident response recommendation to block the attacker's IP string at the edge firewall level.
- Recommended enforcing TLS 1.3 across all internal web server configurations to mandate session encryption and eliminate cleartext vulnerabilities.

---

## 📈 Network Defense Impact
Mastering packet-level analytics allows an analyst to translate raw wire telemetry into business-protecting defensive postures:
- ⏱️ **Root-Cause Accuracy:** Accelerates incident investigation times by extracting definitive indicators of compromise (IoCs) directly from network layer headers.
- 🛡️ **Hardened Perimeter:** Provides network security engineers with the exact protocol definitions required to build zero-trust access control lists (ACLs).
