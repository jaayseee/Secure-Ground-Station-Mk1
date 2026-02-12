# 02 — Threat Model

## Methodology
This threat model uses STRIDE to identify potential threats across trust boundaries defined in the Data Flow Diagram.

STRIDE Categories:
- Spoofing
- Tampering
- Repudiation
- Information Disclosure
- Denial of Service
- Elevation of Privilege

---

## Trust Boundary 1: Untrusted → DMZ

### Threat 1: Malicious File Upload
Category: Tampering  
Description: An attacker uploads a malicious or malformed file to exploit the ingestion service.  
Impact: Remote code execution or pipeline compromise.  
Mitigation: File validation, hashing, size limits, logging.

### Threat 2: API Brute Force
Category: Denial of Service / Spoofing  
Description: External attacker floods ingestion endpoint.  
Impact: Service degradation.  
Mitigation: Rate limiting, firewall rules, logging alerts.

---

## Trust Boundary 2: DMZ → Internal

### Threat 3: Compromised DMZ Service Pivot
Category: Elevation of Privilege  
Description: If ingestion API is compromised, attacker attempts lateral movement to processing zone.  
Impact: Full system compromise.  
Mitigation: Strict firewall deny, no direct DB access.

---

## Trust Boundary 3: Internal → User Access

### Threat 4: Unauthorized Analyst Access
Category: Information Disclosure  
Description: Analyst accesses files beyond authorization.  
Impact: Sensitive data leak.  
Mitigation: RBAC, read-only roles, audit logs.

### Threat 5: Metadata Manipulation
Category: Tampering  
Description: Attacker modifies metadata to hide malicious processing.  
Impact: Integrity loss.  
Mitigation: Access controls, logging, restricted DB access.
