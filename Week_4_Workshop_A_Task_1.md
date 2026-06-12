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

## 3. Detection Triggers

Indicators of Compromise (IoCs) and events that trigger the activation of this IRP include, but are not limited to:

* **Cloud Infrastructure Anomalies:** Unauthorized API calls, unexpected configuration changes in the production environment, or brute-force attempts on root/admin accounts.
* **Data Exfiltration Signals:** Unusual volume of data egress from healthcare databases or unauthorized access to patient records.
* **Malware/Ransomware Alerts:** Endpoint Detection and Response (EDR) alerts signaling active ransomware or malicious binaries within the cloud network.
* **Third-Party Notifications:** Escalations from NHS Trust security operations or threat intelligence feeds regarding compromised MediCore assets.

---

## 4. Containment

Immediate tactical steps to limit the scale and disruption of the incident:

* **Short-Term Isolation:** Isolate affected cloud workloads, compromise user accounts, or virtual networks using automated security groups and IAM policy restrictions.
* **Evidence Preservation:** Take forensic snapshots of affected virtual machine disks and dump volatile memory where applicable before terminating resources.
* **System Backups:** Verify the integrity and isolation of immutable backups to ensure they have not been targeted by the attacker.

---

## 5. Eradication

Steps taken to completely remove the threat from the environment:

* **Vulnerability Remediation:** Identify and patch the initial entry point (e.g., misconfigured cloud storage, unpatched software, or compromised credentials).
* **Threat Removal:** Delete malicious files, revoke compromised API keys/certificates, and force global password resets for impacted accounts.
* **Sanitization Verification:** Run deep security scans across the environment to confirm no residual backdoors or malware remain.

---

## 6. ICO Notification

In accordance with UK GDPR guidelines for data breaches involving Personal Identifiable Information (PII) or protected health information:

* **Reporting Timeline:** The Information Commissioner’s Office (ICO) must be notified without undue delay and, where feasible, not later than **72 hours** after becoming aware of the breach.
* **Submission Channel:** Reports must be officially logged via the [report.ico.org.uk](https://report.ico.org.uk) portal.
* **Content Required:** Description of the nature of the breach, approximate number of data subjects concerned, likely consequences, and measures taken or proposed to mitigate the impact.

---

## 7. Recovery

Restoring systems to secure, normal operations:

* **Phased Restoration:** Restore services from trusted, clean backups or redeploy infrastructure as code (IaC) templates.
* **Enhanced Monitoring:** Implement heightened logging and real-time monitoring on restored assets to catch potential re-infection attempts.
* **NHS Trust Validation:** Coordinate with the affected NHS Trust via secure email within the **4-hour** SLA window to confirm connection safety before restoring federated access.

---

## 8. Lessons Learned

Post-incident review processes to prevent future recurrences:

* **Post-Mortem Meeting:** Hold a mandatory debrief with the Incident Lead, CTO, and DPO within 5 business days of incident closure.
* **Documentation:** Document the root cause, timeline of events, and effectiveness of the response capabilities.
* **Plan Optimization:** Update this IRP document and cloud security controls based on gaps identified during the incident handling process.