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

## 3. Incident Lifecycle Navigation

To ensure rapid execution, the detailed procedures for specific phases of this plan have been modularized into dedicated operational playbooks:

* **Detection & Triggers:** Refer to `DETECTION_TRIGGERS.md` for monitoring rules and UK GDPR Article 32 mapping.
* **Containment & Eradication:** Refer to `INCIDENT_PLAYBOOKS.md` for step-by-step CLI isolation and remediation commands.
* **Regulatory Reporting:** Refer to `BREACH_NOTIFICATION.md` for the strict 72-hour regulatory escalation chain.

---

## 4. Recovery

Restoring systems to secure, normal operations:

* **Phased Restoration:** Restore services from trusted, clean backups or redeploy infrastructure as code (IaC) templates.
* **Enhanced Monitoring:** Implement heightened logging and real-time monitoring on restored assets to catch potential re-infection attempts.
* **NHS Trust Validation:** Coordinate with the affected NHS Trust via secure email within the **4-hour** SLA window to confirm connection safety before restoring federated access.

---

## 5. Lessons Learned

Post-incident review processes to prevent future recurrences:

* **Post-Mortem Meeting:** Hold a mandatory debrief with the Incident Lead, CTO, and DPO within 5 business days of incident closure.
* **Documentation:** Document the root cause, timeline of events, and effectiveness of the response capabilities.
* **Plan Optimization:** Update this IRP document and cloud security controls based on gaps identified during the incident handling process.