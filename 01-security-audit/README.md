# Security Audit — Botium Toys (Internal IT Audit)

**Course:** Google Cybersecurity Professional Certificate — Course 2: Play It Safe: Manage Security Risks

## What This Activity Asked For

This was a guided audit activity based on a fictional company, **Botium Toys** — a small U.S. toy business with a growing online presence (including E.U. customers). The IT manager wanted an internal audit to:

- Assess the company's current security posture using the **NIST Cybersecurity Framework (CSF)**
- Identify which security **controls** were in place or missing
- Assess **compliance** with PCI DSS (payment card data), GDPR (E.U. customer data), and SOC (data integrity/confidentiality)

The task was to review the provided scope, goals, and risk assessment report, then complete a **controls and compliance checklist** based on the details given.

**Given risk score:** 8/10 (high) — due to gaps in controls and compliance adherence.

## Controls Assessment

| Control | In Place? |
|---|---|
| Firewall | ✅ Yes |
| Antivirus software | ✅ Yes |
| Locks (offices, storefront, warehouse) | ✅ Yes |
| CCTV surveillance | ✅ Yes |
| Fire detection/prevention | ✅ Yes |
| Least privilege | ❌ No |
| Separation of duties | ❌ No |
| Disaster recovery plans | ❌ No |
| Backups | ❌ No |
| Password policies | ❌ No |
| Password management system | ❌ No |
| Intrusion detection system (IDS) | ❌ No |
| Encryption | ❌ No |
| Manual monitoring/maintenance for legacy systems | ❌ No |

## Compliance Assessment

**PCI DSS (Payment Card Industry Data Security Standard)** — 0/4 best practices met
- ❌ Only authorized users have access to cardholder data
- ❌ Credit card data stored/processed/transmitted in a secure environment
- ❌ Data encryption procedures implemented
- ❌ Secure password management policies adopted

**GDPR (General Data Protection Regulation)** — 2/4 best practices met
- ❌ E.U. customer data kept private/secured
- ✅ 72-hour breach notification plan in place
- ❌ Data properly classified and inventoried
- ✅ Privacy policies/procedures enforced

**SOC (System and Organization Controls)** — 1/4 best practices met
- ❌ User access policies established
- ❌ Sensitive data (PII/SPII) kept confidential/private
- ✅ Data integrity ensured
- ❌ Data available only to authorized individuals

## Key Takeaways

- Botium Toys has decent **physical security** (locks, CCTV, fire systems) and basic **perimeter/endpoint defense** (firewall, antivirus) — but almost no **data protection or access control** in place.
- The complete absence of encryption, least privilege, and password policy enforcement is the most serious gap — especially given they process credit card data and E.U. customer data.
- PCI DSS compliance is essentially at 0%, which is a significant liability given they accept online payments.

## Recommendations

*The course marked this section optional — I've drafted it based on my findings below.*

Based on the audit findings, I would prioritize the following for Botium Toys' IT manager, ranked by risk severity:

1. **Classify assets** — before controls can be properly scoped, Botium Toys needs to classify its assets (e.g., what data is sensitive/high-risk vs. low-risk). Without this, it's difficult to know exactly where controls like least privilege and encryption need to be applied first.
2. **Implement encryption for cardholder data** — this is a PCI DSS baseline requirement and currently completely absent; highest priority given they process payments directly.
3. **Enforce least privilege and separation of duties** — currently all employees can access cardholder data and customer PII/SPII, which is a major exposure if any single account is compromised.
4. **Adopt a strong password policy with a centralized password management system** — current policy is below modern minimum standards, and the lack of centralized management is already creating operational friction (frequent reset tickets).
5. **Establish disaster recovery plans and regular backups** — there is currently no way to recover from data loss, ransomware, or system failure.
6. **Deploy an Intrusion Detection System (IDS)** — the firewall alone cannot detect threats that get past the perimeter.
7. **Formalize legacy system monitoring** — set a defined schedule and clear intervention procedures instead of ad hoc maintenance.


---
*Part of [security-projects](../).*
