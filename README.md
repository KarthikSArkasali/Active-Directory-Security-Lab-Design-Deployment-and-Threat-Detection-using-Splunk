# Active Directory Security: Deployment, Monitoring with Splunk, and Attack Simulation

## Project Objective
The objective of this project is to **design, build, and secure a complete Active Directory (AD) environment** in a virtual lab setting. It focuses on hands-on implementation of cybersecurity principles, including:

- **Designing a logical AD architecture** with clearly defined roles and network segmentation
- **Deploying and configuring virtual machines** for endpoint, domain controller, attacker, and log analysis roles
- **Instrumenting Windows systems with Sysmon and Splunk** to generate and collect rich security telemetry
- **Installing and managing Active Directory**, including user and organizational unit setup
- **Simulating real-world attacks** using Kali Linux and Atomic Red Team to test security posture
- **Detecting and analyzing malicious activity in Splunk** using Windows Event IDs and MITRE ATT&CK mappings

This project enhances skills in AD administration, threat detection, SIEM integration, and cybersecurity monitoring in enterprise-like environments.

## 🚀 Step 1: Logical Architecture  
 ![AD Project](https://github.com/user-attachments/assets/7c7c3952-39e0-43cb-be46-573c25a9c8eb)
- Created a high‑level diagram in Draw.io showing VM roles, network segments, and Splunk infrastructure.

## 💻 Step 2: VM Deployment  
| VM Name      | OS             | Role                   |
|--------------|----------------|------------------------|
| `Target-PC`  | Windows 10     | Endpoint for testing   |
| `AD-Server`  | Windows Server | Domain Controller      |
| `Ubuntu-VM`  | Ubuntu Linux   | Splunk Indexer/Forwarder |
| `Kali-VM`    | Kali Linux     | Attack Platform        |

![Virtual Machines](https://github.com/user-attachments/assets/351792a7-830d-4ce6-94b5-30d10e717ae8)


## 🔧 Step 3: Sysmon & Splunk Setup  
- **Sysmon** installed on both `Target-PC` and `AD-Server`  
- **Splunk Universal Forwarder** deployed on Windows hosts  
- Verified Splunk Forwarder service was running and sending events  

| VM           | Tool                | Status              |
|--------------|---------------------|---------------------|
| Target‑PC    | Sysmon & Splunk UF  | ✅ Forwarder active |
| AD‑Server    | Sysmon & Splunk UF  | ✅ Forwarder active |

![Splunk Forwarder](https://github.com/user-attachments/assets/bdd16c60-ba1a-4e4c-8999-0fb287674d9f)

## 🏗 Step 4: Active Directory Installation  
1. Promoted `AD-Server` to domain controller for `karthik.domain`  
2. Created OUs and test users:  
   - **HR** →  `sahanaA`
   - **IT** →  `vijayaA` 

### 1. Organizational Unit HR: 

![HR](https://github.com/user-attachments/assets/06834537-9eb4-498c-bb6e-ae00d89a776f)

### 2. Organizational Unit IT: 

![IT](https://github.com/user-attachments/assets/bb01c6a6-0145-49b1-b304-32e089b992d7)


## 🛡 Step 5: Attack Simulation & Telemetry Analysis  

### 5.1 RDP Brute‑Force (Kali → Target‑PC)  
- Launched Hydra against RDP on `Target-PC`  
- **Splunk** detected Event ID **4625** (failed logins) and **4624** (successful logins)  

| Event ID | Description               | Count |
|----------|---------------------------|-------|
| 4625     | Failed login attempts     |  49   |
| 4624     | Successful login attempts |   1   |

#### 1. RDP Brute‑Force (Kali → Target‑PC)
![RDP Brute](https://github.com/user-attachments/assets/a42ada35-a4bf-4498-b8d3-4d901951ed45)

#### 2. Event ID 4625(failed logins):

![4625 Count](https://github.com/user-attachments/assets/ab1f6fb0-1cc1-4928-b8a8-b589aa2ec13d)

#### 3. Event ID 4624(successful logins):

![Successful login](https://github.com/user-attachments/assets/5f82705a-5e4e-475f-a03c-95dd9222feed)


### 5.2 Atomic Red Team (ART) Testing  
- Installed ART on `Target-PC`  
- Executed tests for:
  - **T1136.001** – Create Local Account  
  - **T1059.001** – Command & Scripting Interpreter  
  - **PowerShell** activity  

#### 1. Create Local Account (T1136.001) 
![T1136 001](https://github.com/user-attachments/assets/c9013d1f-e0dd-4ef2-9414-a0f1f750aaff)

#### 2. Command & Scripting Interpreter (T1059.001)
![T1059 001](https://github.com/user-attachments/assets/91c57db3-f7a2-4882-a01f-81dfa7a8621b)

#### 3.  Powershell Activity
![Powershell](https://github.com/user-attachments/assets/dd312e15-f256-4f58-adfc-47a5ee9b5fde)


## 🔍 What You’ll Learn  
- Designing a secure AD topology  
- Instrumenting Windows hosts for rich telemetry  
- Collecting and visualizing security events in Splunk  
- Simulating real‑world attacks and validating detection  
- Mapping ATT&CK techniques to actual log events  




