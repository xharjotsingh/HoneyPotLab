
# project-guide.md — Steps to Build Honeypot SOC Lab on Azure

---

## Step 1 — Infrastructure Setup

1. Create a **Resource Group** (serves as a container for all lab resources).
2. Create a **Virtual Network** and place it in the same Resource Group.
3. Create a **Virtual Machine** (your honeypot) using a Windows image.
   - Avoid obvious names like “honeypot”; use something subtle like `corp-east1`.
   - You can use the template provided in: docs/Virtual-Machine-Template
4. Modify the **Network Security Group (NSG)** for the VM:
   - Add an **inbound rule**: allow any traffic from any source and any ports. (Rule: `AllowAnyCustomAnyInbound`)
5. RDP into the VM and **disable Windows Defender Firewall**:
   - Navigate: Windows Defender Firewall → Firewall Properties → Turn off Domain, Private, and Public profiles.

---

## Step 2 — Network Validation and Failed Login Simulation

6. From your host machine, **ping the public IP** of the VM to verify internet connectivity.
7. Turn off the remote connection temporarily, then **intentionally try logging in with bad credentials** to trigger security logs.
   - Verify log entries under: `Event Viewer → Windows Logs → Security`
   - Example reference:../docs/screenshots/Intentional-FailedLoginAttempts.png

---

## Step 3 — Log Analytics + Sentinel Configuration

8. Create a **Log Analytics Workspace** (this will store all logs).
9. Create a **Microsoft Sentinel** instance connected to that workspace.
   - Go to **Content Hub** in Sentinel.
   - Search for **Windows Security Events** → Install → Click *Manage*.
   - Enable **Windows Security Events via AMA (Azure Monitoring Agent)**.
   - Create a **Data Collection Rule**.

---

## Step 4 — Watchlist + Threat Detection

10. Ensure logs are successfully flowing into the Sentinel workspace.
11. Create a **Watchlist** in Sentinel:
    - Set *Source Type* to: `Azure Storage`
    - Use the file from: ../watchlist/geoip-watchlist-LINK
    - Set *SearchKey* to: `network`

12. Write and test a **KQL query** to detect attackers based on geo IP:
    - Query location: /kql/GeoIP.kql

---

## 🔹 Step 5 — Workbook Visualization

13. In Sentinel, create a new **Workbook**:
    - Delete all pre-populated elements.
    - Click `+ Add` → Select **Add query**.
    - Go to **Advanced Editor** → 
    Paste JSON from: ../workbook/AttackMap-JSON
    - This will create an **interactive attacker map** visualization based on geolocation.

---
