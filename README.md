# Azure-Secure-Cloud-Foundation-and-Threat-Detection
To design, deploy, and secure a baseline Azure environment from the ground up. Implement robust identity controls, segment a virtual network, secure storage assets, and establish a continuous security monitoring and incident response baseline.

---

**Major Phases**
Identity & Access Management (IAM): Securing the human and non-human perimeter.

Network Security: Designing a segmented, firewalled virtual network.

Data Protection: Securing storage and managing cryptographic keys.

Security Posture & Monitoring: Centralizing logs and evaluating compliance.

Threat Detection & Response: Deploying a SIEM and simulating an attack.

Documentation & Portfolio Assembly: Translating technical work into professional assets.


---


**Technologies Used**
Microsoft Entra ID (formerly Azure AD): Users, Groups, RBAC, Conditional Access/MFA.

Azure Networking: Virtual Networks (VNet), Subnets, Network Security Groups (NSGs).

Azure Storage & Key Vault: Blob storage, encryption, secrets management.

Microsoft Defender for Cloud: Cloud Security Posture Management (CSPM), vulnerability assessments.

Microsoft Sentinel (SIEM): Log ingestion, Kusto Query Language (KQL), threat hunting.


---

**Skills Implemented**
Implementing Principle of Least Privilege via Azure RBAC.

Architecting secure network boundaries and micro-segmentation.

Securing cloud storage against public exposure and data exfiltration.

Centralizing audit logs using Log Analytics Workspaces.

Deploying and configuring a modern SIEM.

Executing basic Incident Response workflows (Alert triage and investigation).

Creating professional architecture diagrams and technical documentation.

---


**Project Roadmap**
Stage 1: Establishing the Identity Perimeter (Users, Groups, Custom RBAC Roles, and enforcing MFA).

Stage 2: Building a Defensible Network Architecture (VNet creation, isolating subnets, configuring NSGs, and verifying blocked traffic).

Stage 3: Securing Data Assets (Deploying a Storage Account, disabling public access, configuring Key Vault, and setting up logging).

Stage 4: Enabling Visibility and Posture Management (Setting up Log Analytics, onboarding Defender for Cloud, and reviewing security recommendations).

Stage 5: SIEM Deployment and Incident Simulation (Deploying Microsoft Sentinel, generating a malicious event, and investigating the alert).

Stage 6: Portfolio Polish (Finalizing diagrams, writing the README, and extracting resume bullets).


---

**Stage 1: Establishing the Identity Perimeter** 

Objectives:
Establish a secure identity foundation by creating isolated user accounts, organizing them into logical groups, applying the Principle of Least Privilege (PoLP) through role assignments, and enforcing Multi-Factor Authentication (MFA).

1.Create the Users:
Log in to the Azure Portal using your root/free-tier account.Search for and navigate to Microsoft Entra ID.

Under the Manage menu, select Users > All users > New user > Create new user.

Create a user named sec-admin (e.g., User principal name: sec-admin@yourtenant.onmicrosoft.com). 

Set a secure password and copy it down. 

Repeat the process to create a second user named auditor.

<img width="952" height="612" alt="image" src="https://github.com/user-attachments/assets/fb83449a-c09d-470b-bbb8-55e75dec1b7b" />
