# MediCore IRP — Containment & Eradication Playbooks

> **CRITICAL EXECUTION RULE:** Phase 3 containment actions must begin within **15 minutes** of alert validation. Written step-by-step procedures must be followed exactly to prevent hesitation during off-hours incidents.

---

## Containment (Phase 3) — Risk R01: Unauthorised SSH Access

### 1. PRESERVE Logs First (Forensic Isolation)
Before modifying the state of the asset or cutting off network access, export volatile log data to ensure the attacker's footprint is preserved for analysis.
* **AWS Environment:** Export CloudWatch logs to a secured S3 bucket:
  ```bash
  aws logs create-export-task --task-name "R01-SSH-Forensics" --log-group-name "/aws/vendedlogs/vpc" --from $(date -d '1 hour ago' +%s*1000) --to $(date +%s*1000) --destination "secure-forensics-bucket"