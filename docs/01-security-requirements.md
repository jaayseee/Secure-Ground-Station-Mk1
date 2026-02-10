# 01 — Security Requirements

## Network Segmentation & Access Control
SR-01: The system shall implement separate network zones for Management, DMZ (Ingestion), Processing, Data Storage, and Analyst Access.
SR-02: External/untrusted sources shall only communicate with the Ingestion service in the DMZ and shall have no direct access to Processing or Data Storage zones.
SR-03: Administrative access to any server shall be restricted to the Management network via a hardened jump host.
SR-04: The Processing zone shall not accept inbound connections from the Analyst zone or from external sources.
SR-05: Firewall rules shall explicitly deny all traffic by default and allow only documented required flows (least privilege networking).
SR-06: East-west traffic between internal zones (Processing ↔ Data) shall be restricted to required ports and known hosts only.

## Identity, Authentication, Authorization
SR-07: All user access to the Analyst portal/API shall require authentication.
SR-08: Analyst users shall have read-only access to processed data outputs.
SR-09: Service-to-service communication (Ingestion → Processing, Processing → Storage) shall use dedicated service identities (not personal accounts).
SR-10: Administrative actions shall be auditable and tied to a unique admin identity.

## Data Protection
SR-11: Raw uploads shall be treated as untrusted until validated; validated files shall be moved to a controlled staging area before processing.
SR-12: The Data Storage zone shall not be directly accessible from the DMZ.
SR-13: Sensitive configuration values (e.g., API keys) shall not be stored in source code and shall be provided via environment variables or a secrets mechanism.
SR-14: Data retention requirements shall be documented for raw data, processed data, and logs.

## Logging & Monitoring
SR-15: All security-relevant events (auth attempts, file uploads, processing actions, admin changes) shall be logged with timestamps and source identifiers.
SR-16: Logs from all zones shall be centralized to a monitoring system to support investigation.
SR-17: The system shall alert on suspicious activity, such as repeated failed logins or unexpected access attempts between zones.

## Secure Configuration & Vulnerability Management
SR-18: Systems shall implement secure baseline configurations (e.g., reduce unnecessary services, least privilege, patching plan).
SR-19: The environment shall support vulnerability scanning of key hosts and tracking of findings to remediation actions.
SR-20: The project shall include a security validation plan and report demonstrating that key requirements have been verified.

