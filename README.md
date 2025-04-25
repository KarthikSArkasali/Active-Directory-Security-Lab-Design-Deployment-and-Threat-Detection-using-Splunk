# Active Directory Security: Deployment, Monitoring with Splunk, and Attack Simulation

This project demonstrates how to build and secure an Active Directory environment end‑to‑end. You’ll:

1. **Design** the logical architecture  
2. **Deploy** virtual machines  
3. **Instrument** Windows endpoints with Sysmon & Splunk  
4. **Install** and configure Active Directory  
5. **Test** security using brute‑force attacks (Kali) and Atomic Red Team  
6. **Analyze** telemetry in Splunk

## 🚀 Step 1: Logical Architecture  
 ![Logical Diagram](images/ad-logical-diagram.png)  
Created a high‑level diagram in Draw.io showing VM roles, network segments, and Splunk infrastructure.

## 💻 Step 2: VM Deployment  
| VM Name      | OS             | Role                   |
|--------------|----------------|------------------------|
| `Target-PC`  | Windows 10     | Endpoint for testing   |
| `AD-Server`  | Windows Server | Domain Controller      |
| `Ubuntu-VM`  | Ubuntu Linux   | Splunk Indexer/Forwarder |
| `Kali-VM`    | Kali Linux     | Attack Platform        |

## 🔧 Step 3: Sysmon & Splunk Setup  
- **Sysmon** installed on both `Target-PC` and `AD-Server`  
- **Splunk Universal Forwarder** deployed on Windows hosts  
- Verified Splunk Forwarder service was running and sending events  

| VM           | Tool                | Status              |
|--------------|---------------------|---------------------|
| Target‑PC    | Sysmon & Splunk UF  | ✅ Forwarder active |
| AD‑Server    | Sysmon & Splunk UF  | ✅ Forwarder active |

## 🏗 Step 4: Active Directory Installation  
1. Promoted `AD-Server` to domain controller for `karthik.domain`  
2. Created OUs and test users:  
   - **HR** → `vijayaA`  
   - **IT** → `sahanaA`  

![AD OUs](images/ad-ous.png)

## 🛡 Step 5: Attack Simulation & Telemetry Analysis  

### 5.1 RDP Brute‑Force (Kali → Target‑PC)  
- Launched Hydra against RDP on `Target-PC`  
- **Splunk** detected Event ID **4625** (failed logins) and **4624** (successful logins)  

| Event ID | Description               | Count |
|----------|---------------------------|-------|
| 4625     | Failed login attempts     |  37   |
| 4624     | Successful login attempts |   1   |

### 5.2 Atomic Red Team (ART) Testing  
- Installed ART on `Target-PC`  
- Executed tests for:
  - **T1136.001** – Create Local Account  
  - **T1059.001** – Command & Scripting Interpreter  
  - **PowerShell** activity  

![ART Events in Splunk](images/art-events.png)

## 🔍 What You’ll Learn  
- Designing a secure AD topology  
- Instrumenting Windows hosts for rich telemetry  
- Collecting and visualizing security events in Splunk  
- Simulating real‑world attacks and validating detection  
- Mapping ATT&CK techniques to actual log events  




