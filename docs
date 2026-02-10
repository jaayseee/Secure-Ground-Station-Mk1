# 00 — Scope

## 1. Purpose
This project designs and prototypes a secure "ground station" environment for Earth observation systems. The system securely ingests imagery data, processes it, stores outputs, and provides controlled analyst access, with security requirements and validation artefacts.

## 2. In Scope
- Secure ingestion endpoint (DMZ)
- Processing pipeline (internal processing zone)
- Storage for raw + processed data (data zone)
- Analyst portal/API access (analyst zone)
- Central logging/monitoring (security visibility)
- Security engineering artefacts (requirements, architecture, threat model, TRA, test plan/report)

## 3. Out of Scope
- Real satellite hardware, radios, antennas
- Real SAR signal processing accuracy (we simulate processing)
- Full enterprise identity infrastructure (we can simulate RBAC)
- Production-grade HA/DR (documented as future work)

## 4. Users and Roles
- Admin: manages systems (restricted to management network / jump host)
- Operator/Service: ingestion + processing services (service accounts)
- Analyst: read-only access to processed outputs

## 5. Assets to Protect
- Imagery data (raw + processed)
- Credentials (API keys, service accounts)
- Processing infrastructure and configurations
- Logs (audit trail) and monitoring data

## 6. Assumptions
- Lab environment (VMware-based when implemented)
- Internal analyst network is trusted but not “fully safe”
- External upload source is untrusted until verified
- Security logging is required for investigation and accountability

## 7. Constraints
- Open-source or free tools where possible
- Must be reproducible in a single lab environment
- Minimize complexity while preserving realistic security patterns

