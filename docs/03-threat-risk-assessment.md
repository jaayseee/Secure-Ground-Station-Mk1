# 03 — Threat Risk Assessment (TRA)

## Risk Rating Methodology

Risk = Likelihood × Impact

Likelihood Levels:
1 – Low (unlikely, requires significant effort)
2 – Medium (possible with moderate effort)
3 – High (easily achievable or common attack)

Impact Levels:
1 – Low (limited operational disruption)
2 – Medium (service disruption or data integrity impact)
3 – High (major compromise, sensitive data loss, system takeover)

Risk Levels:
1–2 = Low
3–4 = Medium
6–9 = High


## Risk Assessment Table

| ID | Threat | Category | Likelihood | Impact | Risk Score | Risk Level | Mitigation | Residual Risk |
|----|--------|----------|------------|--------|------------|------------|------------|---------------|
| R1 | Malicious file upload to ingestion API | Tampering | 3 | 3 | 9 | High | File validation, hashing, size limits, logging | Medium |
| R2 | Brute force / API flooding | DoS | 3 | 2 | 6 | High | Rate limiting, firewall rules, monitoring alerts | Low |
| R3 | Compromised DMZ service pivot to internal | Elevation of Privilege | 2 | 3 | 6 | High | Strict firewall segmentation, no DB access from DMZ | Low |
| R4 | Unauthorized analyst data access | Information Disclosure | 2 | 3 | 6 | High | RBAC, read-only roles, audit logs | Low |
| R5 | Metadata tampering in DB | Tampering | 2 | 2 | 4 | Medium | Restricted DB access, logging, integrity controls | Low |
| R6 | Internal service credential exposure | Spoofing | 2 | 3 | 6 | High | Environment variables, no hardcoded secrets | Low |
| R7 | Lack of logging prevents incident response | Repudiation | 2 | 2 | 4 | Medium | Centralized logging + retention policy | Low |


## High Risk Items Summary

The highest risk items involve untrusted input and potential lateral movement:

- R1 (Malicious file upload): Direct exposure to untrusted input makes this the primary risk vector.
- R2 (Denial of Service): Public-facing services are vulnerable to flooding attempts.
- R3 (DMZ Pivot): Segmentation is critical to prevent escalation from compromised edge services.

Mitigation strategies focus on strict network segmentation, validation controls, and least privilege principles.
