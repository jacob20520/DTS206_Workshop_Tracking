# MediCore Health Systems — Incident Response Plan

**Version:** 1.0  
**Date:** June 2026  
**Owner:** Lead Cloud Security Architect  

---

## 1. Purpose

The purpose of this Incident Response Plan (IRP) is to establish a structured, repeatable, and compliant framework for detecting, containing, eradicating, and recovering from security incidents at MediCore Health Systems. This plan ensures minimizing operational disruption, protecting sensitive patient data, and meeting legal and regulatory compliance obligations (including UK GDPR and NHS Data Security and Protection Toolkit standards).

---

## 2. Roles + Contacts

The following matrix outlines the key personnel, communication channels, and Service Level Agreements (SLAs) required for mobilizing the incident response team.

| Role | Title | Channel | SLA |
| :--- | :--- | :--- | :--- |
| **Incident Lead** | Cloud Security Architect | Teams | 15 min |
| **DPO** | External DPO | Direct phone | 2 hours |
| **CTO** | Chief Technology Officer | Teams | 2 hours |
| **ICO** | Information Commissioner | report.ico.org.uk | 72 hours |
| **NHS Trust** | Per contract | Secure email | 4 hours |

---

## 3. Detection Triggers & GDPR Mapping

In compliance with **GDPR Article 32(1)(b)**—which mandates the ongoing confidentiality, integrity, availability, and resilience of processing systems—the following monitoring rules serve as our technical detection mechanisms.

### Trigger & Phase Mapping Matrix

| Alert Description | Triggered Phase | Notification Recipients | Response SLA | Relevant GDPR / Compliance Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Alert 1:** CPU > 80% for 3+ min | **Phase 1: Detection / Phase 2: Containment** | Incident Lead | 15 min | **Art. 32(1)(b) - Availability & Resilience:** Detects potential DoS/DDoS attacks or runaway processes threatening service availability. |
| **Alert 2:** 3+ failed SSH logins in 5 min | **Phase 1: Detection** | Incident Lead + CTO | 5 min | **Art. 32(1)(c) - Ability to Restore & Protect:** Identifies active brute-force or unauthorized access attempts before a breach occurs. |
| **Alert 3:** DB access not from web tier | **Phase 2: Containment** | DPO | **IMMEDIATE** | **Art. 32(1)(a) / Art. 33 - Confidentiality:** Indicates a severe architectural bypass. Potential active data exfiltration triggering immediate DPO assessment for data breach reporting. |
| **Alert 4:** Patient data access outside 22:00-06:00 | **Phase 2: Containment** | DPO + CTO | **IMMEDIATE** | **Art. 32 - Confidentiality & Least Privilege:** Anomalous after-hours access to sensitive health data. Requires instant triage to determine if credential theft has occurred. |
| **Alert 5:** Storage access outside VNet | **Phase 2: Containment** | Incident Lead | 10 min | **Art. 32(1)(b) - Integrity Failures:** Detects network perimeter breaches or misconfigured cloud storage exposed to the public internet. |

### Technical Compliance Justification

* **GDPR Article 32 (Security of Processing):** Our automated CloudWatch / Azure Monitor alerting metrics directly satisfy the legal requirement to maintain continuous visibility over system integrity. Failing to monitor these specific vectors constitutes a failure to implement appropriate technical and organizational measures.
* **GDPR Article 33 (Notification to ICO):** Alerts marked as **IMMEDIATE** (Alerts 3 and 4) involve direct risk to protected health data. These alerts immediately loop in the Data Protection Officer (DPO) to start the 72-hour assessment window required for regulatory notification.

---

## 4. Containment (Phase 3) — Risk Playbooks

> **CRITICAL EXECUTION RULE:** Phase 3 containment actions must begin within **15 minutes** of alert validation. Written step-by-step procedures must be followed exactly to prevent hesitation during off-hours incidents.

### Risk R01: Unauthorised SSH Access

#### 1. PRESERVE Logs First (Forensic Isolation)
Before modifying the state of the asset or cutting off network access, export volatile log data to ensure the attacker's footprint is preserved for analysis.
* **AWS Environment:** Export CloudWatch logs to a secured S3 bucket:
  ```bash
  aws logs create-export-task --task-name "R01-SSH-Forensics" --log-group-name "/aws/vendedlogs/vpc" --from $(date -d '1 hour ago' +%s*1000) --to $(date +%s*1000) --destination "secure-forensics-bucket"