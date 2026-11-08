# Incident Handler's Journal — Course 6 Capstone

**Course:** Google Cybersecurity Professional Certificate — Course 6: Sound the Alarm — Detection and Response

## What This Activity Asked For

This capstone activity asked me to keep an incident handler's journal across Course 6 — logging findings after each hands-on activity and tool exploration, using the course's template (Date, Entry #, Description, Tool(s) Used, the Five W's, Additional Notes). Some entries document an actual incident scenario (where the Five W's apply), while others are notes on learning a new tool (where the Five W's are marked N/A, since no real incident was involved). The journal closes with a short Reflections section on the course as a whole.

## Journal Entries

| # | Date | Activity | NIST IR Phase | Tool(s) |
|---|---|---|---|---|
| 1 | Oct 24, 2026 | Documented a ransomware incident at a healthcare clinic | Post-Incident Activity | None |
| 2 | Oct 26, 2026 | Analyzed a packet capture file | Detection and Analysis | Wireshark |
| 3 | Oct 27, 2026 | Captured and analyzed live network traffic | Detection and Analysis | tcpdump |
| 4 | Oct 29, 2026 | Investigated the file hash of a suspicious file | Detection and Analysis | VirusTotal |
| 5 | Nov 1, 2026 | Reviewed an incident's final report | Post-Incident Activity | None |
| 6 | Nov 4, 2026 | Explored signatures and logs | Detection and Analysis | Suricata |
| 7 | Nov 6, 2026 | Queried events | Detection and Analysis | Splunk |
| 8 | Nov 7, 2026 | Queried events | Detection and Analysis | Google SecOps (Chronicle) |

### Entry #1 — Ransomware Incident at a Healthcare Clinic

**Phase:** Post-Incident Activity · **Tool(s):** None

| 5 W | Detail |
|---|---|
| **Who** | An organized group of unethical hackers known to target the healthcare and transportation industries |
| **What** | A ransomware attack — the clinic's files were encrypted, with a ransom note demanding payment for the decryption key |
| **When** | Tuesday morning, approximately 9:00 a.m. |
| **Where** | A small U.S. healthcare clinic specializing in primary-care services |
| **Why** | A phishing email with a malicious attachment, which encrypted the clinic's files once opened |

**Notes:** Two open questions came out of documenting this one — how the clinic could prevent a repeat of this attack, and whether paying the ransom to recover the decryption key would even be the right call.

### Entry #2 — Packet Capture Analysis (Wireshark)

**Phase:** Detection and Analysis · **Tool(s):** Wireshark

This was a tool-exploration activity rather than a real incident, so the Five W's don't apply here. Wireshark's GUI made it straightforward to inspect packet data and apply filters to sort through it efficiently — useful for pulling out details like source/destination IP, port, protocol, and MAC address when investigating potentially malicious activity.

### Entry #3 — Live Traffic Capture (tcpdump)

**Phase:** Detection and Analysis · **Tool(s):** tcpdump

Also a tool-exploration activity — captured live traffic, saved it to a file, then analyzed the capture for network traffic details. tcpdump's command-line interface was a steeper learning curve than Wireshark's GUI, but it gives more granular control over what's captured.

### Entry #4 — Suspicious File Hash Investigation (VirusTotal)

**Phase:** Detection and Analysis · **Tool(s):** VirusTotal

| 5 W | Detail |
|---|---|
| **Who** | A malicious actor |
| **What** | A malicious payload executed on an employee's computer |
| **When** | A sequence from 1:11 p.m.–1:20 p.m.: email received (1:11) → attachment downloaded and opened (1:13) → unauthorized executable files created (1:15) → IDS detects the files and alerts the SOC (1:20) |
| **Where** | A financial services company |
| **Why** | An employee opened a malicious email attachment, which executed the payload; an IDS then flagged the resulting executable files and alerted the SOC analyst |

**Notes:** Once the file was confirmed malicious, the response followed the organization's existing playbook for this scenario — a reminder of how following a playbook's defined steps helps minimize impact and shorten response time. The open question from this entry: would phishing-awareness training for employees be enough on its own to stop this type of attack going forward?

### Entry #5 — Final Report Review

**Phase:** Post-Incident Activity · **Tool(s):** None

| 5 W | Detail |
|---|---|
| **Who** | Attributed to a vulnerability in the company's e-commerce web application, rather than a named actor |
| **What** | An employee received an email from an external address claiming customer data had been stolen, demanding $25,000 in cryptocurrency to avoid releasing it publicly |
| **When** | December 28, 2022, 7:20 p.m. PT |
| **Where** | A mid-sized retail company |
| **Why** | A vulnerability in the e-commerce application allowed a forced-browsing attack — the attacker modified the order number in a purchase-confirmation URL to access and exfiltrate other customers' transaction data |

**Notes:** This activity was about reviewing and learning how to structure a final report, not producing one from scratch. Based on the root cause described, the kind of security measures that would have helped here are vulnerability scanning, penetration testing, allow-listing, and enforcing least privilege.

### Entry #6 — Signatures and Logs (Suricata)

**Phase:** Detection and Analysis · **Tool(s):** Suricata

Tool-exploration activity. Suricata runs off a custom signature file configured to the organization's needs; it applies those rules to traffic passing through the monitored interface to decide whether a packet should trigger an alert, then writes the results to an output log for filtering and analysis.

### Entry #7 — Querying Events (Splunk)

**Phase:** Detection and Analysis · **Tool(s):** Splunk

Tool-exploration activity. Splunk uses its own query language, Search Processing Language (SPL), which supports chaining multiple commands and arguments together to narrow down and analyze event data.

### Entry #8 — Querying Events (Google SecOps / Chronicle)

**Phase:** Detection and Analysis · **Tool(s):** Google SecOps (Chronicle)

Tool-exploration activity. Google SecOps offers two ways to search for events: a **UDM Search**, which queries data that's already been ingested, parsed, and normalized (faster, since it's searching structured/indexed data), and a **Raw Log Search**, which searches the raw, unparsed logs directly (slower, but necessary when the normalized data doesn't have what's needed).

## Reflections

**Which activity was most challenging, and why?**
tcpdump. Coming from a GUI-based tool like Wireshark, switching to a command-line interface was a real learning curve — getting comfortable with the syntax took deliberately slowing down and reading the instructions carefully rather than rushing through them.

**How has my understanding of incident detection and response changed?**
Going into this course, I had a surface-level sense of what detection and response meant. By the end, I had a much clearer picture of the full lifecycle — how the phases connect, why plans/processes/people all matter as much as the tools, and how a SOC actually works through an incident from first alert to final report.

**Which tool or concept did I enjoy the most, and why?**
SIEM tools. Watching how a SIEM pulls log data in from multiple sources, normalizes it, and centralizes it on a single dashboard — with the ability to visualize it as charts — stood out as directly relevant to the day-to-day work of a SOC analyst, which is why I spent extra time with it.

---
📄 [View original document](Portfolio%20Activity%206.pdf)

*Part of [security-projects](../).*
