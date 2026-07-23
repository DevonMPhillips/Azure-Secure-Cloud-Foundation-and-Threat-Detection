# Azure Secure Cloud Foundation and Threat Detection

Designed, deployed, and secured a baseline Azure environment from the ground up. Implementing identity controls, segmented virtual networks, secured storage assets, and established a continuous security monitoring and incident response baseline.

---

### Major Phases

- Identity & Access Management: Securing the human and non-human perimeter.

- Network Security: Designing a segmented, firewalled virtual network.

- Data Protection: Securing storage and managing cryptographic keys.

- Security Posture & Monitoring: Centralizing logs and evaluating compliance.

- Threat Detection & Response: Deploying a SIEM and simulating an attack.

<br>

---

### Technologies Used

- Microsoft Entra ID: Users, Groups, RBAC, Conditional Access/MFA.

- Azure Networking: Virtual Networks, Subnets, Network Security Groups.

- Azure Storage & Key Vault: Blob storage, encryption, secrets management.

- Microsoft Defender for Cloud: Cloud Security Posture Management, vulnerability assessments.

- Microsoft Sentinel: Log ingestion, Kusto Query Language (KQL), threat hunting.

<br>

---

### Skills Implemented

- Implementing Principle of Least Privilege via Azure RBAC.

- Architecting secure network boundaries and micro-segmentation.

- Securing cloud storage against public exposure and data exfiltration.

- Centralizing audit logs using Log Analytics Workspaces.

- Deploying and configuring a Microsoft Sentinel SIEM.

- Executing basic Incident Response workflows.

- Creating professional architecture diagrams and technical documentation.

<br>


# Project Walkthrough - Full

Below are the detailed steps I've taken to complete this project.


### Project Roadmap

- Stage 1: Establishing the Identity Perimeter. Users, Groups, Custom RBAC Roles, and enforcing MFA.

- Stage 2: Building a Defensible Network Architecture. VNet creation, isolating subnets, configuring NSGs, and verifying blocked traffic.

- Stage 3: Securing Data Assets. Deploying a Storage Account, disabling public access, configuring Key Vault, and setting up logging.

- Stage 4: Enabling Visibility and Posture Management. Setting up Log Analytics, onboarding Defender for Cloud, and reviewing security recommendations.

- Stage 5: SIEM Deployment and Incident Simulation. Deploying Microsoft Sentinel, generating a malicious event, and investigating the alert.

<br>

<br>

## Stage 1: Establishing the Identity Perimeter


### Objectives:

- Establish a secure identity foundation by creating isolated user accounts, organizing them into logical groups, applying the Principle of Least Privilege through role assignments, and enforcing Multi-Factor Authentication.

<br>

#### 1. Create the Users:

Log in to the Azure Portal.

Search for and navigate to **Microsoft Entra ID**.

Under the Manage menu, select **Users** > **All users** > **New user** > **Create new user**.

Create a user named **sec-admin**. 

Set a secure password. 

Repeat the process to create a second user named **auditor**.

<br>

<img width="952" height="612" alt="image" src="https://github.com/user-attachments/assets/fb83449a-c09d-470b-bbb8-55e75dec1b7b" />

<br>

<img width="1001" height="277" alt="image" src="https://github.com/user-attachments/assets/accebb81-a8fd-4eaa-9dfb-17974abb9d2e" />

#### 2. Create Security Groups: 

Navigate back to the Entra ID overview and **select** Groups > **New group**.

Group type: Security.

Group name: Cloud-Security-Admins. Leave membership type as **Assigned**.

Under Members, add the sec-admin user. Click **Create**.

Create a second group named Auditors and add the auditor user to it.

<br>

<img width="1090" height="670" alt="image" src="https://github.com/user-attachments/assets/3ee2894f-3586-4c42-9729-dc1bac6e9f73" />

<br>

#### 3. Assign Entra ID Roles: Granting tenant-level permissions.

In Entra ID, go to **Roles and administrators**. 

Search for the **Global Reader** role. Click on it

Select **Add assignments**, and assign it to the **Security-Auditors** group. 

Search for the **Security Administrator** role and assign it to the **Cloud-Security-Admins** group.

<br>

<img width="1092" height="667" alt="image" src="https://github.com/user-attachments/assets/015c2fbe-5c51-4c52-85a5-47a7580852d0" />

<br>

<img width="1092" height="667" alt="image" src="https://github.com/user-attachments/assets/13396251-cea4-4298-8fa5-285c5b30f337" />

<br>

#### 4. Enforce Multi-Factor Authentication. 

In the Entra ID overview menu, scroll down to **Properties**.

At the bottom of the page, click the link for **Manage security defaults**. Ensure the toggle is set to **Enabled**.

Click **Save**. Now all users in the tenant are now required to register for MFA using the Microsoft Authenticator app.

<br>

<img width="1092" height="862" alt="image" src="https://github.com/user-attachments/assets/148b134c-bb2c-4ec9-89eb-32ae9fc9b7cb" />

<br>

<br>

## Stage 2: Building a Defensible Network Architecture


### Objectives:

- Designed a secure network foundation by deploying an Azure Virtual Network, segmenting it into public-facing and private tiers, and implementing strict traffic control using Network Security Groups.

<br>

### Architecture Overview:

I built a Two-Tier architecture. I will created a VNet containing two subnets: Subnet-Web for simulated public-facing web servers and Subnet-Database for simulated backend data servers.

I then attach an NSG to each subnet. The Web NSG will only allow HTTP/HTTPS from the internet. The Database NSG will completely block the internet and only accept traffic originating from the Web subnet.

### Services Used:

- Azure Resource Groups
- Azure Virtual Networks
- Azure Network Security Groups


#### 1. Create a Resource Group:

In the Azure Portal, **search** for Resource groups. Click **Create**.

Name it RG-SecureCloud-Prod.

Select a region close to you (e.g., East US).

Click **Review + create**, then **Create**.

<br>

<img width="720" height="215" alt="image" src="https://github.com/user-attachments/assets/9edd6436-cab5-4f58-8463-56b97cf325f4" />

<br>

#### 2. Deploy the Virtual Network and Subnets:

**Search** for Virtual Networks and click **Create**.

**Select** RG-SecureCloud-Prod as the Resource Group.

Name it **VNet-Core**. Go to the IP Addresses tab. Azure usually defaults to a 10.0.0.0/16 space with a default subnet.

**Delete** the **default** subnet.

Click **Add** subnet. Name it **Subnet-Web** with an address range of 10.0.1.0/24. Click **Add**.

Click **Add** subnet again. Name it **Subnet-Database** with an address range of 10.0.2.0/24. Click **Add**.

Click **Review + create**, then **Create**.

<br>

<img width="1917" height="772" alt="image" src="https://github.com/user-attachments/assets/c7c49144-0a38-46af-88a8-482f1e400b97" />

<br>

<img width="1092" height="622" alt="image" src="https://github.com/user-attachments/assets/bc714430-b357-44ca-8b39-ee011747c15a" />

<br>

<img width="1241" height="97" alt="image" src="https://github.com/user-attachments/assets/156a8786-150b-4945-bd25-2d5a26c89a9d" />

<br>

#### 3. Create Network Security Groups: Creating the boundary firewalls.

Search for Network security groups and click **Create**.

Select the **RG-SecureCloud-Prod** resource group. Name the **NSG NSG-Web-Tier** and click **Create**.

Repeat this process to create a second NSG named **NSG-Database-Tier**.

<br>

#### 4. Configure Security Rules: Applying Least Privilege to network traffic. 

Navigate to NSG-Web-Tier. Under Settings, click **Inbound security rules.** 

<br>

Add a rule to allow HTTPS: 

| Property | Configuration | Purpose |
|---|---|---|
| Rule Name | Allow-HTTPS-Inbound | Identifies the purpose of the security rule |
| Source | Any | Allows inbound HTTPS requests from external sources |
| Source Port Range | * | Allows traffic from any originating port |
| Destination | Any | Applies rule to all resources associated with the NSG |
| Destination Port | 443 (HTTPS) | Allows secure web traffic using HTTPS protocol |
| Protocol | TCP | HTTPS communication uses TCP |
| Action | Allow | Permits HTTPS inbound connections |
| Priority | 100 | Determines rule processing order (lower numbers take priority) |

<br>

<img width="1092" height="827" alt="image" src="https://github.com/user-attachments/assets/335402fc-7530-415a-8afc-144658017423" />


<br>

Go to Inbound security rules.

**Add** a rule to only **allow** traffic from the Web Subnet:

<br>

| Property | Configuration | Purpose |
|---|---|---|
| Rule Name | Allow-SQL-From-Web | Identifies the purpose of the network security rule |
| Source | IP Address: 10.0.1.0/24 (Web Subnet) | Restricts SQL access to only approved web-tier resources |
| Source Port Range | * | Allows connections from any originating port |
| Destination | Any | Applies the rule to resources protected by the NSG |
| Destination Port Range | 1433 (SQL Server) | Allows Microsoft SQL Server communication |
| Protocol | TCP | SQL Server uses TCP for database communication |
| Action | Allow | Permits approved database connections |
| Priority | 110 | Evaluated before broader deny rules |

<br>

<img width="1092" height="861" alt="image" src="https://github.com/user-attachments/assets/2892e18d-75b5-4d87-8300-1e9edf5283f4" />

<br>

**Add** a second rule to explicitly **deny** all other VNet traffic to the database:

<br>

| Property | Configuration | Purpose |
|---|---|---|
| Rule Name | Deny-Other-VNet-Traffic | Identifies the purpose of the network security rule |
| Source | VirtualNetwork | Applies the rule to traffic originating from resources within the virtual network |
| Source Port Range | * | Applies to traffic from any source port |
| Destination | Any | Applies to all resources protected by the NSG |
| Destination Port Range | * | Applies to all destination ports |
| Protocol | Any | Applies to all network protocols |
| Action | Deny | Blocks unauthorized network communication |
| Priority | 4000 | Evaluated after specific allow rules but before default NSG rules |
| Network Security Group | NSG-Database-Tier | Applies segmentation controls to the database tier |

<br>

<img width="1091" height="865" alt="image" src="https://github.com/user-attachments/assets/f5b801c2-ff2f-4af5-8aac-d178fc546273" />

<br>

#### 5. Associate NSGs to Subnets: Binding the firewalls to the network segments.

While still in NSG-Database-Tier, click Subnets under Settings.

Click **Associate**, select **VNet-Core**, and select **Subnet-Database**.

Navigate back to NSG-Web-Tier, click **Subnets**, and associate it with **Subnet-Web.**

<br>
  
<img width="1091" height="862" alt="image" src="https://github.com/user-attachments/assets/30bf0216-92a5-43f0-9cc0-ec0cc21f5363" />

<br>

<img width="1095" height="335" alt="image" src="https://github.com/user-attachments/assets/480f9b8f-a572-4d7e-8150-a29715658cf9" />

<br>

<img width="1092" height="862" alt="image" src="https://github.com/user-attachments/assets/c41d0540-0b90-4005-8314-5cf77e425962" />

<br>

## Stage 3: Securing Data Assets

### Objectives

- Deployed a cloud storage solution and a secrets management vault, hardening both against unauthorized access, public exposure, and accidental data loss

### Architecture Overview

I deployed an Azure Storage Account simulating where my web application stored user uploads. I then  explicitly blocked all anonymous public access and enable retention policies to recover deleted data. Then, I deployed an Azure Key Vault to act as a secure safe for the application's database credentials, using Azure RBAC to control who can view the secrets.

#### 1. Deploy a Hardened Storage Account:

In the Azure Portal, search for Storage accounts and click **Create**.

Select your **RG-SecureCloud-Prod** resource group. 

**Storage account name**: This must be globally unique across all of Azure 

**Region**: Choose the same region as my VNet.

**Performance**: Standard (keeps costs at zero). 

**Redundancy**: Locally-redundant storage (LRS).

Go to the Advanced tab. Ensure **Require secure transfer for REST API operations** is checked. 

CRITICAL: Uncheck **Allow enabling anonymous access on individual containers.** This enforces a tenant-level block on public exposure. 

Minimum TLS version: Version 1.2. 

Click Review, then Create.

<br>

<img width="1095" height="615" alt="image" src="https://github.com/user-attachments/assets/b7db723d-0601-447a-ae3c-10fd5e9c98df" />

<br>

#### 2. Configure Data Protection (Soft Delete): Protecting against accidental or malicious deletion. 

Once the Storage Account deploys, navigate to it. 

In the left menu under Data management, select **Data protection.** 

Under Recovery, ensure **Enable soft delete for blobs** and **Enable soft delete for containers** are both checked.

Set the retention policy to **7 days** (sufficient for this project).

Click **Save** at the top.

<br>

<img width="1091" height="817" alt="image" src="https://github.com/user-attachments/assets/a07054d5-6a9e-43bd-a686-d598cccec712" />

<br>

#### 3. Deploy Azure Key Vault: 

Search for Key vaults and click **Create**. 

Select your **RG-SecureCloud-Prod** resource group. 

Key vault name: Must also be globally unique.

Region: Same as my VNet. 

Pricing tier: Standard.

Go to the Access configuration tab. 

- CRITICAL: Change the Permission model from Vault access policy to Azure **role-based access control.**

Click **Review + create**, then **Create.**

<br>

<img width="1092" height="506" alt="image" src="https://github.com/user-attachments/assets/7a381eba-afff-41e5-966c-13665ae491ab" />

<br>

#### 4. Assign Key Vault RBAC Roles:

Navigate to your newly created Key Vault.

Click on **Access control (IAM)** in the left menu.

Click **Add** > **Add role assignment.**

Search for the Key Vault Secrets Officer role (this allows creating and managing secrets). 

<br>

<img width="1096" height="610" alt="image" src="https://github.com/user-attachments/assets/0f0bec36-0007-4c31-b293-27549f41b102" />

<br>

Select it and click **Next.**

Under Members, click **Select members**, search for the **sec-admin user**, and select them.

Click **Review + assign.**

<br>

<img width="1090" height="606" alt="image" src="https://github.com/user-attachments/assets/4bdd0e02-de2f-4ab6-86c3-aff14b0ae82b" />

<br>

#### 5. Create a Test Secret:

Log in as the sec-admin user for this step, or assign the role to my current root account as well. 

In the Key Vault, select **Secrets** under Objects. 

Click **Generate/Import. **

## Azure Key Vault Secret

<br>

| Property | Configuration |
|---|---|
| Secret Name | DB-Password |
| Secret Value | `<Replace-With-Test-Password>` |

Click **Create.**

<br>

<img width="1092" height="866" alt="image" src="https://github.com/user-attachments/assets/0dcac49d-03e1-4815-984a-33270df1efe0" />

<br>

### Stage 4: Enabling Visibility and Posture Management

### Objectives

- Deployed a centralized logging repository to collect audit trails, configured resources to forward logs, and enabled Cloud Security Posture Management to continuously assess the environment for misconfigurations.

### Architecture Overview

- I created a Log Analytics Workspace (LAW-SecureCloud). Then went back to the Key Vault I built in Stage 3 and configure its "Diagnostic Settings" to forward all audit logs to this workspace. Finally, I activated the free foundational tier of Microsoft Defender for Cloud to scan my subscription and generate a Secure Score.

### Services Used

- Azure Log Analytics Workspace
- Microsoft Defender for Cloud (Foundational CSPM)

#### 1. Create a Log Analytics Workspace:

In the Azure Portal, search for Log Analytics workspaces and click Create. 

Select your **RG-SecureCloud-Prod** resource group. 

Name it **LAW-SecureCloud.** 

Region: Choose the same region you have been using. 

Click **Review + Create**, then **Create.**

<br>

<img width="1097" height="637" alt="image" src="https://github.com/user-attachments/assets/6c6c7a23-4492-43a9-8b0b-c715a236f814" />

<br>


#### 2. Configure Diagnostic Settings for Key Vault:

Navigate back to your Key Vault.

In the left menu, scroll down to the Monitoring section and select **Diagnostic settings.**

Click **Add diagnostic setting.** 

Setting name: Send-Audit-to-LAW.

Under Logs, check the box for audit as this tracks who accesses the vault.

Under Destination details, check **Send to Log Analytics workspace.**

Select your subscription and choose **LAW-SecureCloud** from the dropdown.

Click **Save** at the top.

<br>

<img width="1092" height="637" alt="image" src="https://github.com/user-attachments/assets/4d2c83fb-1077-4b51-a5c4-b1bd920c7c11" />

<br>


#### 3. Generate Audit Logs:

While still in the Key Vault, go to **Secrets** under Objects.

Click on the **DB-Password** secret you made earlier.

Click on the current version of the secret.

Click **Show Secret Value.** (This action creates an audit event recording that your user account viewed the secret).

<br>

#### 4. Onboard Defender for Cloud:

Search for **Microsoft Defender for Cloud** in the top search bar.

In the left menu, scroll down to Management and click **Environment settings.**

Click on your Azure Subscription.

In the Defender plans page, look at the Foundational CSPM (Cloud Security Posture Management) tier. Ensure its status is **On**.

We will strictly use the Foundational/Free tier for this project.

<br>

Verification & Testing

Verify Log Ingestion:

Navigate to your **LAW-SecureCloud** workspace.

Under General, select **Logs.**

In the query window, type the following Kusto Query Language (KQL) command:

```
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
```

<br>

<img width="1051" height="852" alt="image" src="https://github.com/user-attachments/assets/a698eead-213d-4546-899a-ff523df2cdbb" />

<br>

You should see the audit logs generated when you viewed the secret.

<br>

<img width="1917" height="860" alt="image" src="https://github.com/user-attachments/assets/be9b6321-a697-4750-9546-8109d571706d" />

<br>


## Stage 5: SIEM Deployment and Incident Simulation

### Objectives

- Deployed a Security Information and Event Management (SIEM) solution, created a custom detection rule using KQL, simulated a security event, then executed basic incident response workflows.

### Architecture Overview

- Microsoft Sentinel does not store data itself; it sits on top of the Log Analytics Workspace (LAW-SecureCloud) I built in Stage 4. I activated Sentinel on that workspace. Then, I wrote a Analytics Rule that constantly scans the incoming AzureDiagnostics logs. If it sees an event where someone views your Key Vault secret, it fired an alert and generated an Incident ticket for me to investigate.

#### 1. Onboard Microsoft Sentinel:

In the Azure Portal search bar, type Microsoft Sentinel and select it. Click Create (or Add).

You will see a list of available workspaces. Select the LAW-SecureCloud workspace you created in Stage 4. 

Click Add. Within a few moments, the Sentinel dashboard will load.

<img width="952" height="867" alt="image" src="https://github.com/user-attachments/assets/33a91428-89a2-44a6-9a19-b2cb883dd3b7" />

#### 2. Create a Custom Analytics Rule:

In the Microsoft Sentinel left menu, under Configuration, click Analytics.

Click Create at the top, then select Scheduled query rule. 

General Tab:

- Name: Key Vault Secret Accessed
  
- Description: Detects when a user views the plain-text value of a Key Vault secret.
  
- Tactics: Select Credential Access.
  
- Severity: Medium.
  
- Click Next.

<br>

Set rule logic Tab: 

In the Rule query box, paste the following KQL command:

<br>

```
kqlAzureDiagnostics
  | where ResourceProvider == "MICROSOFT.KEYVAULT"
  | where OperationName == "SecretGet"
```
  
Scroll down to Query scheduling. Set **Run query** every to 5 minutes and **Lookup data** from the last to 5 minutes.

Click **Next.**

Incident settings Tab: Ensure Create incidents from alerts triggered by this analytics rule is Enabled.

Click **Review + create**, then click **Save**.

<br>

<img width="955" height="865" alt="image" src="https://github.com/user-attachments/assets/255eeffe-d65d-4b26-9d8b-315a294ab1e9" />

<br>


#### 3. Simulate the Attack:

Open a new tab and navigate back to the Key Vault.

Go to **Secrets** under Objects and click the DB-Password secret.

Click the current version, then click **Show Secret Value.**

This action generates the SecretGet event your new Sentinel rule is actively looking for.

<br>

<img width="957" height="866" alt="image" src="https://github.com/user-attachments/assets/dbd8e552-122e-44a3-b542-23bfe180ce65" />

<br>


#### 4. Investigate and Close the Incident:

Go back to your Microsoft Sentinel tab.

In the left menu, under Threat management, click **Incidents.**

Wait a few minutes. 

Your Key Vault Secret Accessed incident will appear in the queue.

Click on the incident to open the details pane on the right. 

Click **View full details.**

Review the timeline and the raw logs to confirm it was your user account that triggered it.

Change the Status dropdown from **New** to **Closed.**

Select the classification **True Positive** - Suspicious activity and **add a comment**: "Testing custom analytics rule. Confirmed alert fired successfully upon secret access."

If the incident appears in the Sentinel queue and you are successfully able to close it with a classification, the SIEM pipeline is working flawlessly.

<br>

<img width="956" height="865" alt="image" src="https://github.com/user-attachments/assets/f35f0b75-d8c4-4b40-81c5-c827cc1eb400" />

<br>

<img width="956" height="861" alt="image" src="https://github.com/user-attachments/assets/1e94ae49-d980-4ffc-9f4d-fe11d54c8065" />
