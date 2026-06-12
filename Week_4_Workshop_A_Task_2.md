# MediCore IRP — Detection Triggers & GDPR Mapping

In compliance with **GDPR Article 32(1)(b)**—which mandates the ongoing confidentiality, integrity, availability, and resilience of processing systems—the following monitoring rules serve as our technical detection mechanisms.

## Trigger & Phase Mapping Matrix

| Alert Description | Triggered Phase | Notification Recipients | Response SLA | Relevant GDPR / Compliance Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Alert 1:** CPU > 80% for 3+ min | **Phase 1: Detection / Phase 2: Containment** | Incident Lead | 15 min | **Art. 32(1)(b) - Availability & Resilience:** Detects potential DoS/DDoS attacks or runaway processes threatening service availability. |
| **Alert 2:** 3+ failed SSH logins in 5 min | **Phase 1: Detection** | Incident Lead + CTO | 5 min | **Art. 32(1)(c) - Ability to Restore & Protect:** Identifies active brute-force or unauthorized access attempts before a breach occurs. |
| **Alert 3:** DB access not from web tier | **Phase 2: Containment** | DPO | **IMMEDIATE** | **Art. 32(1)(a) / Art. 33 - Confidentiality:** Indicates a severe architectural bypass. Potential active data exfiltration triggering immediate DPO assessment for data breach reporting. |
| **Alert 4:** Patient data access outside 22:00-06:00 | **Phase 2: Containment** | DPO + CTO | **IMMEDIATE** | **Art. 32 - Confidentiality & Least Privilege:** Anomalous after-hours access to sensitive health data. Requires instant triage to determine if credential theft has occurred. |
| **Alert 5:** Storage access outside VNet | **Phase 2: Containment** | Incident Lead | 10 min | **Art. 32(1)(b) - Integrity Failures:** Detects network perimeter breaches or misconfigured cloud storage exposed to the public internet. |

---

## Technical Compliance Justification

* **GDPR Article 32 (Security of Processing):** Our automated CloudWatch / Azure Monitor alerting metrics directly satisfy the legal requirement to maintain continuous visibility over system integrity. Failing to monitor these specific vectors constitutes a failure to implement appropriate technical and organizational measures.
* **GDPR Article 33 (Notification to ICO):** Alerts marked as **IMMEDIATE** (Alerts 3 and 4) involve direct risk to protected health data. These alerts immediately loop in the Data Protection Officer (DPO) to start the 72-hour assessment window required for regulatory notification.