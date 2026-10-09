# Incident Report Analysis — ICMP Flood (DoS/DDoS) Attack

**Course:** Google Cybersecurity Professional Certificate — Course 3: Connect and Protect: Networks and Network Security

## What This Activity Asked For

This was a guided portfolio activity using the **NIST Cybersecurity Framework (CSF)** to analyze a network security incident. The scenario: a multimedia company's internal network went down for two hours after a flood of ICMP packets overwhelmed an unconfigured firewall, causing a denial-of-service condition. The task was to break the incident down using the CSF's core functions — Identify, Protect, Detect, Respond, Recover — and produce an incident report plus a forward-looking security improvement plan.

## Incident Report (NIST CSF)

**Summary**
The company experienced a security event when all internal network services suddenly stopped responding. Investigation found the cause was a flood of incoming ICMP packets — a Denial-of-Service (DoS) style attack — exploiting an unconfigured firewall. The incident management team responded by blocking incoming ICMP packets, stopping all non-critical network services, and restoring critical services. The attack disrupted the network for two hours before resolution.

**Identify**
A malicious actor sent a flood of ICMP pings through the company's unconfigured firewall, exploiting the lack of rate-limiting or filtering rules. This allowed the attacker to overwhelm the network and deny service to legitimate internal traffic. The entire internal network was affected, and all critical resources needed to be secured and restored.

**Protect** *(preventive controls — stop this from happening again)*
- A new firewall rule to limit the rate of incoming ICMP packets
- An IDS/IPS system configured to filter ICMP traffic based on suspicious characteristics

**Detect** *(detection controls — catch it faster next time)*
- Source IP address verification on the firewall, to check for spoofed IPs on incoming ICMP packets
- Network monitoring software to flag abnormal traffic patterns

**Respond** *(the future response plan, not just what happened this time)*
- Isolate affected systems quickly to prevent further disruption to the network
- Restore critical systems and services first, ahead of non-critical ones
- Analyze network logs for suspicious or abnormal activity to understand scope
- Report incidents to upper management and, where applicable, legal authorities

**Recover**
To recover from an ICMP flood-style DoS/DDoS attack:
1. Block the external ICMP flood at the firewall
2. Stop non-critical network services to reduce internal traffic load
3. Restore critical network services first
4. Once the flood has timed out, bring non-critical systems and services back online

## Reflections / Notes

My first draft of this exercise combined the Protect and Detect sections into one — listing all four security measures together under "Protect." Comparing against the course's exemplar helped clarify an important distinction in the NIST CSF: **Protect** covers controls that actively *prevent* an incident (rate-limiting, IDS/IPS filtering), while **Detect** covers controls that *identify* suspicious activity after the fact (IP verification, traffic monitoring). The two functions serve different purposes in a security program, and conflating them loses that structure.

I also initially wrote the Respond section around the *immediate* containment actions taken during the attack, when the activity was actually asking for a **forward-looking response plan** for *future* incidents — a different (and more useful) deliverable for an incident playbook.

---
📄 [View original document](Portfolio%20Activity%202.pdf)

*Part of [security-projects](../).*
