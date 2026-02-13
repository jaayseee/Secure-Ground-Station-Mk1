# Network Plan

Base Network: 10.0.0.0/16

## Zones and Subnets

Management Zone:
Subnet: 10.0.10.0/24
Gateway: 10.0.10.1 (pfSense)

DMZ (Ingestion):
Subnet: 10.0.20.0/24
Gateway: 10.0.20.1 (pfSense)

Processing Zone:
Subnet: 10.0.30.0/24
Gateway: 10.0.30.1 (pfSense)

Data Zone:
Subnet: 10.0.40.0/24
Gateway: 10.0.40.1 (pfSense)

Analyst Zone:
Subnet: 10.0.50.0/24
Gateway: 10.0.50.1 (pfSense)



## VM IP Assignments

pfSense:
- Management: 10.0.10.1
- DMZ: 10.0.20.1
- Processing: 10.0.30.1
- Data: 10.0.40.1
- Analyst: 10.0.50.1

Jumpbox:
10.0.10.10

Monitoring (Wazuh later):
10.0.10.20

Ingestion API:
10.0.20.10

Processor Worker:
10.0.30.10

MinIO:
10.0.40.10

Postgres:
10.0.40.20

Portal:
10.0.50.10


## VMware Network Mapping

VMnet2 → Management → 10.0.10.0/24
VMnet3 → DMZ → 10.0.20.0/24
VMnet4 → Processing → 10.0.30.0/24
VMnet5 → Data → 10.0.40.0/24
VMnet6 → Analyst → 10.0.50.0/24

VMnet8 (NAT) → External Internet


## pfSense Interface Mapping

WAN → VMware NAT (VMnet8)
OPT1 → Management (VMnet2)
OPT2 → DMZ (VMnet3)
OPT3 → Processing (VMnet4)
OPT4 → Data (VMnet5)
OPT5 → Analyst (VMnet6)


## Firewall Rule Intent

Default: Deny all inter-zone traffic

Allow Rules:

1. External (WAN) → DMZ (10.0.20.10) TCP 80/443
2. Management (10.0.10.0/24) → All Zones TCP 22
3. DMZ (10.0.20.10) → Processing (10.0.30.10) Required app port
4. Processing (10.0.30.10) → Data (10.0.40.10/20) Required ports
5. Analyst (10.0.50.0/24) → Portal (10.0.50.10) HTTPS
6. Portal → Data zone DB port
