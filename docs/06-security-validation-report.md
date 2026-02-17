# 06 – Security Validation Report

## 1. Objective

This report documents validation activities performed to verify implementation of defined security requirements for the Secure Ground Station Architecture (Mk1).

---

## 2. Infrastructure Build & Baseline Configuration

### 2.1 Firewall Deployment

pfSense was deployed as the central segmentation enforcement point with multiple interfaces mapped to distinct security zones.

![Figure 1 – pfSense Dashboard](../evidence/network-build/network-pfsense-dashboard-overview.png)

![Figure 2 – Interface Summary](../evidence/network-build/network-pfsense-interface-summary.png)

### 2.2 Baseline Configuration Controls

DNS, NTP, and interface configuration were verified.

![Figure 3 – General Configuration](../evidence/network-build/network-pfsense-general-config.png)

![Figure 4 – NTP Configuration](../evidence/network-build/network-pfsense-ntp-config.png)

![Figure 5 – LAN Interface Configuration](../evidence/network-build/network-pfsense-lan-config.png)

![Figure 6 – Wizard Completion](../evidence/network-build/network-pfsense-wizard-complete.png)
