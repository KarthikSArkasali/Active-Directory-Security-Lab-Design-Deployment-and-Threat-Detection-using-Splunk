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
 ![1  Block Diagram](https://github.com/user-attachments/assets/83e92b0b-b84e-4b3c-983a-98f7fd3ab9b3)
- Created a high‑level diagram in Draw.io showing VM roles, network segments, and Splunk infrastructure.

## 💻 Step 2: VM Deployment  
| VM Name      | OS             | Role                   |
|--------------|----------------|------------------------|
| `Target-PC`  | Windows 10     | Endpoint for testing   |
| `AD-Server`  | Windows Server | Domain Controller      |
| `Ubuntu-VM`  | Ubuntu Linux   | Splunk Indexer/Forwarder |
| `Kali-VM`    | Kali Linux     | Attack Platform        |

![2  Virtual Machines](https://github.com/user-attachments/assets/82c10b83-4cbc-4930-b177-4590fc1a1042)

## 🔧 Step 3: Sysmon & Splunk Setup  
- **Sysmon** installed on both `Target-PC` and `AD-Server`

![3 1 Sysmon](https://github.com/user-attachments/assets/553966b2-5f34-4496-a61b-2f90cade4727)

- **Splunk Universal Forwarder** deployed on Windows hosts  
- Verified Splunk Forwarder service was running and sending events  

| VM           | Tool                | Status              |
|--------------|---------------------|---------------------|
| Target‑PC    | Sysmon & Splunk UF  | ✅ Forwarder active |
| AD‑Server    | Sysmon & Splunk UF  | ✅ Forwarder active |

![3 2  Splunk Forwarder](https://github.com/user-attachments/assets/4e405cbd-ee9d-42ad-9f0b-e4659a90a42a)

## 🏗 Step 4: Active Directory Installation  
1. Promoted `AD-Server` to domain controller for `karthik.domain`  
2. Created OUs and test users:  
   - **HR** →  `sahanaA`
   - **IT** →  `vijayaA` 

### 1. Organizational Unit HR: 

![4  HR](https://github.com/user-attachments/assets/1993814f-d1d8-4d4f-991e-b9d53b73fa65)

### 2. Organizational Unit IT: 

![5  IT](https://github.com/user-attachments/assets/2bf234b8-8169-440b-bdf2-a62333f8a0a6)

## 🛡 Step 5: Attack Simulation & Telemetry Analysis  

### 5.1 RDP Brute‑Force (Kali → Target‑PC)  
- Launched Hydra against RDP on `Target-PC`  
- **Splunk** detected Event ID **4625** (failed logins) and **4624** (successful logins)  

| Event ID | Description               | Count |
|----------|---------------------------|-------|
| 4625     | Failed login attempts     |  49   |
| 4624     | Successful login attempts |   1   |

#### 1. RDP Brute‑Force (Kali → Target‑PC)
![6  RDP Brute](https://github.com/user-attachments/assets/dbb8c7ac-99e2-4d7e-a932-df26b16adc95)

#### 2. Event ID 4625(failed logins):

![7  4625 Count](https://github.com/user-attachments/assets/3e7c921f-4945-4e80-9721-0e9f3608c43d)

![9  Failed login](https://github.com/user-attachments/assets/910091b8-ccaa-4ecb-8484-3117cb6c82a6)

#### 3. Event ID 4624(successful logins):

![8  Successful login](https://github.com/user-attachments/assets/30ad985f-b835-497e-bb65-be2aaa752f70)

### 5.2 Atomic Red Team (ART) Testing  
- Installed ART on `Target-PC`  
- Executed tests for:
  - **T1136.001** – Create Local Account  
  - **T1059.001** – Command & Scripting Interpreter  
  - **PowerShell** activity  

#### 1. Create Local Account (T1136.001) 
![10  T1136 001](https://github.com/user-attachments/assets/d6385e52-9f08-47bc-b37c-0abbdd6d328a)

#### 2. Command & Scripting Interpreter (T1059.001)
![11  T1059 001](https://github.com/user-attachments/assets/c2988837-4457-40f4-a551-3de479e65684)

#### 3.  Powershell Activity
![12  Powershell](https://github.com/user-attachments/assets/5dd06c30-4874-4ffd-b28e-fd71f8e23552)


## 🔍 What You’ll Learn  
- Designing a secure AD topology  
- Instrumenting Windows hosts for rich telemetry  
- Collecting and visualizing security events in Splunk  
- Simulating real‑world attacks and validating detection  
- Mapping ATT&CK techniques to actual log events  
