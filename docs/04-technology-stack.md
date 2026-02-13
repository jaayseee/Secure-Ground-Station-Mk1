# 04 — Technology Stack & Tooling

## 1. Hardware Environment

### Primary Lab Machine
Device: ASUS ROG Strix (Windows)
- 32 GB RAM
- Multi-core CPU (suitable for virtualization workloads)
- Dedicated GPU (not required but beneficial for performance headroom)

Purpose:
- Hosts VMware lab environment
- Runs pfSense and all virtual machines
- Simulates segmented enterprise network

Reason for Selection:
A high-memory Windows machine allows stable multi-VM lab simulation with proper network segmentation and realistic infrastructure layering.

---

### Secondary Documentation Machine
Device: MacBook Air

Purpose:
- Documentation authoring (Markdown)
- Diagram design (draw.io)
- GitHub management
- Threat modelling and planning

Reason for Separation:
Maintains lab reproducibility and avoids resource contention on the primary virtualization system.


## 2. Virtualization Layer

### VMware Workstation (Windows)

Role:
- Hypervisor for lab environment
- Creates isolated network segments (VMnet interfaces)
- Enables simulation of DMZ, internal zones, and management network

Key Features Used:
- Host-only networks
- NAT networking (WAN simulation)
- Multi-NIC virtual firewall setup
- Snapshotting for rollback testing

Rationale:
VMware provides flexible network segmentation and realistic enterprise lab simulation aligned with environments that use vSphere or ESXi.


## 3. Network & Firewall

### pfSense (Firewall / Router)

Role:
- Central segmentation enforcement
- Default-deny firewall posture
- Inter-zone access control
- Gateway for each subnet

Functions Implemented:
- Multiple interfaces mapped to distinct subnets
- Static IP gateway per zone
- Explicit allow rules for required flows
- Default deny for all other traffic

Security Design Principles:
- Least privilege networking
- Zone-based architecture
- Controlled east-west traffic


## 4. Server Infrastructure (Ubuntu Server)

Each functional component runs on a dedicated Linux VM.

Reason:
- Clear separation of duties
- Simulated microservice-style isolation
- Reduced blast radius in compromise scenarios


## 5. Application Layer

### Ingestion API
Framework: FastAPI (Python)

Role:
- Receives external uploads
- Validates files
- Logs security events
- Passes validated data to processing layer

Security Controls:
- Input validation
- Hashing (SHA-256)
- File size limits
- Logging

---

### Processing Worker
Language: Python

Role:
- Simulates imagery processing
- Writes metadata to database
- Stores processed outputs
- Runs without direct user access

Security Controls:
- No inbound connections from users
- Restricted to internal subnet
- Uses service identity


## 6. Data Storage Layer

### Object Storage
Tool: MinIO

Role:
- Stores raw and processed imagery files
- S3-compatible API
- Accessible only from internal services

---

### Metadata Database
Tool: PostgreSQL

Role:
- Stores metadata (hashes, filenames, timestamps)
- Not accessible from DMZ
- Access restricted via firewall and credentials


## 7. Identity & Access Control

Implementation:
- Role-based access control (RBAC) at application layer
- Read-only analyst role
- Dedicated service accounts for internal services

Security Principles:
- Least privilege
- No hardcoded credentials
- Environment variable-based secret management


## 8. Logging & Monitoring

### Logging Strategy
- JSON structured logs
- Authentication attempts logged
- File uploads logged
- Processing actions logged

### Central Monitoring (Planned Phase)
Tool: Wazuh (future phase)
- Log aggregation
- Alert generation
- Integrity monitoring

Purpose:
To demonstrate auditability and detection capability.


## 9. Vulnerability & Hardening (Planned Validation Phase)

Tools:
- Nmap (network validation)
- OpenVAS or Nessus Essentials (vulnerability scanning)
- Lynis (Linux hardening audit)

Purpose:
- Validate segmentation effectiveness
- Identify misconfigurations
- Document remediation actions


## 10. Documentation & Version Control

- GitHub repository
- Markdown documentation
- Diagrams (draw.io)
- Traceability Matrix (CSV)
- Risk Register (CSV)

Purpose:
To demonstrate engineering lifecycle traceability from requirement → threat → mitigation → validation.
