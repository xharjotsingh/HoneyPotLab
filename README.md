
# Azure Honeypot SOC Lab

## Description

This project sets up a cloud-based Honeypot Security Operations Center (SOC) Lab using Microsoft Azure. It simulates a vulnerable environment to attract and log attacker activity in real-time. The logs are ingested and analyzed in Microsoft Sentinel, enriched with geolocation data, and visualized through a dynamic attack map.

---

## Objectives

- Deploy a public-facing Windows VM as a honeypot to attract attackers.
- Simulate brute-force login attempts to generate authentic security logs.
- Ingest logs into Azure Log Analytics and connect them to Microsoft Sentinel.
- Create a geolocation-based watchlist to enrich attacker data.
- Visualize attack sources with a real-time interactive dashboard using Sentinel Workbooks.

---

## Outcomes

By the end of this project, you will:

- Understand how to build and expose a honeypot securely in Azure.
- Learn how to disable defenses intentionally to attract attackers.
- Monitor and investigate real brute-force attack attempts.
- Correlate attacker IPs with location data using a watchlist.
- Gain experience with KQL, Sentinel Analytics Rules, and Workbook visualizations.

---

## Folder Structure

```
├── docs/
│   ├── screenshots/
│   │   ├── Audit-FailureLogDescription
│   │   ├── CollectionRule-Config
│   │   ├── Intentional-FailedLoginAttempts
│   │   └── VirtualNetwork-Config
│   ├── Virtual-Machine-Template/
│   │   ├── parameters
│   │   └── template
│   └── project-guide.md
│
├── kql/
│   └── GeoIP.kql
│
├── watchlist/
│   └── geoip-watchlist-LINK
│
├── workbook/
│   └── AttackMap-JSON
│
└── README.md
```
Final Attack Map:

<img width="973" height="537" alt="Screenshot 2025-07-27 223955" src="https://github.com/user-attachments/assets/a9b5ae1f-df27-4a0c-ab79-00c0cf6cf63c" />

---

