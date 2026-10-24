<!-- course-title: Professional Cloud Security Engineer Certification Overview -->

<!-- layout: full-bleed -->
# Welcome Slide
![ROI Logo](images/hca-1.png)
---
<!-- layout: title -->
![ROI Logo](images/roi-logo-with-name.png)

# Professional Cloud Security Engineer
# Certification Overview

## Exam scope, domain tour, and a practical preparation path
---
<!-- layout: panel-right -->
# Welcome!

- ROI leads the industry in designing and delivering customized technology and management training solutions
- Meet your instructor
  - Name
  - Background
  - Contact info
- Let’s get started!

![Welcome](images/welcome.png)
---
# Course Objectives

- Orient to the Google Professional Cloud Security Engineer (PCSE) exam: scope, domains, and how to prepare
- Describe the certification’s scope, format, and exam expectations
- Summarize the core exam domains and what each tests
- Identify the highest-yield preparation resources and study path
- Recognize where hands-on experience is required to pass
---
<!-- layout: panel-left -->
# Agenda

- Segment 1: Exam Overview
- Segment 2: Core Domains Tour
- Segment 3: Operations, Compliance, and Prep
- Questions and Answers

![Agenda](images/agenda.png)
---
<!-- layout: panel-right -->
# Who Should Attend

- Cloud security engineers preparing for PCSE
- Security architects validating Google Cloud depth
- Platform engineers expanding into security ownership
- Candidates with Google Cloud project experience seeking a study map

![Who Should Attend](images/who-should-attend.png)
---
<!-- layout: panel-left -->
# Prerequisites

- Prior Google Cloud experience (projects, IAM, networking basics)
- Foundational security knowledge (identity, encryption, logging)
- Helpful: Associate Cloud Engineer or equivalent hands-on background
- Helpful: exposure to Security Command Center and VPC design

![Prerequisites](images/prerequisites.png)
---
<!-- layout: navigation -->
# Course Roadmap

- **Exam Overview**
- Core Domains Tour
- Operations, Compliance, and Prep
---
# What the Certification Validates

- **Access and Identity Management:** Configure IAM roles, policies, and service accounts
- **Network and Boundary Protection:** Implement VPC security, firewalls, and Cloud Armor
- **Data Protection and Encryption:** Manage KMS keys, DLP, and encryption standards
- **Security Operations and Monitoring:** Utilize Security Command Center, logging, and threat detection
- **Compliance and Governance:** Enforce security controls and audit compliance frameworks

> [!NOTE]
> Always verify details against the current official Google Cloud exam guide: blueprints refresh over time.
---
<!-- layout: title-image -->
# Exam at a Glance

![PCSE exam at a glance](images/pcse-exam-at-a-glance.png)
---
<!-- layout: title-image -->
# Domain Map (Approximate Weights)

![PCSE exam domains](images/pcse-exam-domains.svg)
---
<!-- layout: navigation -->
# Course Roadmap

- Exam Overview
- **Core Domains Tour**
- Operations, Compliance, and Prep
---
<!-- layout: title-image -->
# Section 1: Configuring Access (~25%)

![IAM resource hierarchy](images/pcse-iam-hierarchy.png)
---
# Configuring Access: Key Exam Topics

- Resource hierarchy: org → folders → projects → resources
- Least privilege with predefined/custom roles and conditions
- Service accounts, impersonation, and keyless patterns
- Federation/workforce identity concepts at a design level
- Organization Policy constraints that enforce guardrails

| Theme | Example decision |
| :--- | :--- |
| Hierarchy | Where to bind a role for inheritance |
| SA security | Avoid user-managed keys when possible |
| Org policy | Restrict public IPs / SA key creation |
---
# Section 1 Practice Question

**Your organization runs CI/CD pipelines in an external OIDC-compatible platform and needs to deploy workloads to Google Cloud. Security policy prohibits exporting long-lived credentials. What should you configure?**

A. Create a service account, export a JSON key, and store it in the CI/CD platform’s secret store with a 90-day rotation reminder

B. Configure Workload Identity Federation to exchange external OIDC tokens for short-lived Google Cloud credentials and enforce `constraints/iam.disableServiceAccountKeyCreation`

C. Grant the CI/CD developer group the `roles/owner` primitive role on the target project and require 2-Step Verification

D. Store a user-managed service account key in Secret Manager and allow the external pipeline to download it over a public IP
---
# Section 1 Practice Question: Answer

**Your organization runs CI/CD pipelines in an external OIDC-compatible platform and needs to deploy workloads to Google Cloud. Security policy prohibits exporting long-lived credentials. What should you configure?**

**Correct: B.** Configure Workload Identity Federation to exchange external OIDC tokens for short-lived Google Cloud credentials and enforce `constraints/iam.disableServiceAccountKeyCreation`

- Workload Identity Federation eliminates exported service account keys by exchanging trusted external OIDC/SAML tokens for short-lived credentials
- Enforcing `constraints/iam.disableServiceAccountKeyCreation` via Organization Policy prevents teams from creating new user-managed keys
- Rotating or storing exported JSON keys (A, D) still leaves long-lived static credentials that can be leaked
- Granting `roles/owner` (C) violates least privilege
---
<!-- layout: title-image -->
# Sections 2 and 3: Network and Data Protection

![Network and data protection](images/pcse-network-data.png)
---
<!-- layout: 2-column -->
# Section 2: Securing Communications and Boundary Protection (~22%)

### Expect Coverage Of
- VPC firewalls/NGFW ideas
- Segmentation (Shared VPC, peering)
- IAP for admin access patterns
- Cloud Armor/edge protections
- Private Google Access, PSC, VPN/Interconnect
- VPC Service Controls perimeters

### Mindset
- Identity + network together
- Default-deny where sensible
- Private paths over public exposure
---
# Section 2 Practice Question

**Engineers need SSH access to Linux VMs in a production VPC to perform maintenance. Company policy forbids external IP addresses on VMs and prohibits deploying self-managed bastion hosts. How should you enable access?**

A. Configure Identity-Aware Proxy (IAP) TCP forwarding, allow ingress on port 22 from `35.235.240.0/20`, and grant authorized engineers `roles/iap.tunnelResourceAccessor`

B. Enable Private Google Access on the subnet and create a VPC firewall rule allowing SSH from `0.0.0.0/0`

C. Attach ephemeral external IPs to the VMs only during maintenance windows and remove them afterward

D. Configure Cloud NAT on the subnet so external engineers can initiate inbound SSH connections to the private VMs
---
# Section 2 Practice Question: Answer

**Engineers need SSH access to Linux VMs in a production VPC to perform maintenance. Company policy forbids external IP addresses on VMs and prohibits deploying self-managed bastion hosts. How should you enable access?**

**Correct: A.** Configure Identity-Aware Proxy (IAP) TCP forwarding, allow ingress on port 22 from `35.235.240.0/20`, and grant authorized engineers `roles/iap.tunnelResourceAccessor`

- IAP TCP forwarding provides zero-trust administrative access to private VMs without public IPs or bastion hosts
- Firewall rules only need to allow TCP port 22 from Google’s IAP forwarding range (`35.235.240.0/20`), not the open internet
- Private Google Access (B) is for private VMs reaching Google APIs, and `0.0.0.0/0` violates boundary security
- Cloud NAT (D) only supports outbound connections initiated by private VMs, not inbound administrative access
---
<!-- layout: 2-column -->
# Section 3: Ensuring Data Protection (~23%)

### Expect Coverage Of
- Encryption at rest / in transit
- Cloud KMS, CMEK, HSM patterns
- Envelope encryption concepts
- Sensitive Data Protection / DLP
- Dataset access patterns (e.g., BigQuery)
- Securing AI/ML data paths (newer emphasis)

### Mindset
- Who holds keys?
- Where does data leave?
- How is sensitive data discovered?
---
# Network and Data Study Priorities

- **Master VPC Service Controls:** Know how perimeters, access levels, and ingress/egress rules prevent data exfiltration
- **Layer network boundaries:** Practice choosing between Shared VPC, VPC peering, IAP, Cloud Armor, and Private Service Connect
- **Know encryption key ownership:** Distinguish default Google-managed keys, CMEK, CSEK, Cloud EKM, and Cloud HSM trade-offs
- **Automate sensitive data discovery:** Pair Sensitive Data Protection (DLP) inspection and de-identification with BigQuery policy tags

> [!TIP]
> Sections 1, 2, and 3 represent roughly 70% of the exam: deepen IAM, VPC-SC, and KMS until trade-offs feel automatic.
---
# Section 3 Practice Question

**A healthcare analytics team stores patient records in BigQuery. Analysts must query the table for reporting, but only the compliance team may view Social Security numbers (SSNs) in cleartext, while analysts see masked values. What should you configure?**

A. Export the table to Cloud Storage, run a custom Python script to strip SSNs, and load a separate table for analysts

B. Apply BigQuery column-level security using Data Catalog policy tags with a dynamic data masking rule on the SSN column, and grant `Fine-Grained Reader` only to the compliance group

C. Encrypt the BigQuery dataset with a Customer-Managed Encryption Key (CMEK) and revoke the analysts’ Cloud KMS CryptoKey Encrypter/Decrypter role

D. Enable VPC Service Controls around the project and grant the analysts `roles/bigquery.dataOwner`
---
# Section 3 Practice Question: Answer

**A healthcare analytics team stores patient records in BigQuery. Analysts must query the table for reporting, but only the compliance team may view Social Security numbers (SSNs) in cleartext, while analysts see masked values. What should you configure?**

**Correct: B.** Apply BigQuery column-level security using Data Catalog policy tags with a dynamic data masking rule on the SSN column, and grant `Fine-Grained Reader` only to the compliance group

- Policy tags with dynamic data masking allow analysts to query the table without failing while masking sensitive columns (such as SSNs)
- Granting `Fine-Grained Reader` on the policy tag gives the compliance group cleartext access to the same single source of truth
- Duplicating tables via custom scripts (A) adds operational overhead and data drift
- Revoking CMEK access (C) blocks dataset queries entirely rather than selectively masking a column
---
<!-- layout: navigation -->
# Course Roadmap

- Exam Overview
- Core Domains Tour
- **Operations, Compliance, and Prep**
---
# Section 4: Managing Operations (~19%)

- Detect and respond using Google Cloud security operations tooling
- Security Command Center findings, priorities, and remediation workflows
- Logging, monitoring, and detection design (what to log; where to sink)
- Incident-oriented scenarios: investigate → contain → improve controls

| Ops theme | Why it’s tested |
| :--- | :--- |
| SCC | Centralize posture and findings |
| Logging | Evidence + detection inputs |
| Automation | Scale response consistently |
---
# Section 4 Practice Question

**Your security operations team must retain all Admin Activity and Data Access audit logs across 150 projects in your Google Cloud organization for 7 years in immutable storage for forensic investigations. What is the recommended design?**

A. Create a log sink in each of the 150 projects that exports logs to a standard Cloud Storage bucket with Object Versioning enabled

B. Configure an organization-level aggregated log sink (`--include-children`) routing audit logs to a centralized Cloud Storage bucket with a retention policy and locked Bucket Lock

C. Rely on the default `_Required` log bucket in each project, which retains all audit logs indefinitely at no cost

D. Export logs from each project to Pub/Sub and have engineers manually download daily archives to local workstations
---
# Section 4 Practice Question: Answer

**Your security operations team must retain all Admin Activity and Data Access audit logs across 150 projects in your Google Cloud organization for 7 years in immutable storage for forensic investigations. What is the recommended design?**

**Correct: B.** Configure an organization-level aggregated log sink (`--include-children`) routing audit logs to a centralized Cloud Storage bucket with a retention policy and locked Bucket Lock

- An organization-level aggregated sink with `--include-children` automatically captures logs from existing and newly created child projects
- A Cloud Storage bucket with a locked retention policy (Bucket Lock) enforces WORM (write-once, read-many) immutability for compliance and forensics
- The `_Required` bucket (C) only retains logs for 400 days and does not include Data Access audit logs
- Per-project manual sinks (A, D) create operational toil and risk missing new projects
---
<!-- layout: 2-column -->
# Section 5: Supporting Compliance Requirements (~11%)

### What It Covers
- Mapping controls to requirements
- Shared responsibility clarity
- Assured/compliance-oriented offerings at a conceptual level
- Evidence from configs, logs, and policies

### How to Study
- Know *which Google Cloud controls* support common goals
- Don’t memorize every regulation clause
- Tie answers back to hierarchy, network, data, ops
---
# Section 5 Practice Question

**A public-sector customer must run a workload in Google Cloud that requires strict US data residency, US-only Google support personnel access, and automated enforcement of FedRAMP High controls. What should you recommend?**

A. Create a standard Google Cloud folder, apply `constraints/gcp.resourceLocations` set to `in:us-locations`, and open a support ticket requesting US-only engineers

B. Provision an Assured Workloads folder configured for the FedRAMP High compliance regime in the required US region

C. Deploy the workload in a standalone project using Customer-Supplied Encryption Keys (CSEK) and disable Cloud Logging

D. Configure VPC Firewall rules to block non-US IP ranges and grant `roles/viewer` to external auditors
---
# Section 5 Practice Question: Answer

**A public-sector customer must run a workload in Google Cloud that requires strict US data residency, US-only Google support personnel access, and automated enforcement of FedRAMP High controls. What should you recommend?**

**Correct: B.** Provision an Assured Workloads folder configured for the FedRAMP High compliance regime in the required US region

- Assured Workloads enforces data residency, personnel access controls (such as US-person support), KM/encryption requirements, and Organization Policy guardrails for regulated regimes like FedRAMP, CJIS, and IL4
- `constraints/gcp.resourceLocations` alone (A) restricts where resources are created, but does not enforce Google support personnel residency or full regime guardrails
- Disabling Cloud Logging (C) or filtering client IPs (D) does not satisfy cloud provider compliance or sovereignty controls
---
<!-- layout: title-image -->
# High-Yield Study Path

![PCSE study path](images/pcse-study-path.png)
---
# Highest-Yield Preparation Resources

1. **Official exam guide:** Source of truth for domains and in-scope topics
2. **Google Skills labs:** Hands-on experience is essential
3. **Architecture Center security patterns:** Identify best practices
4. **Practice exams and sample questions:** Timing and scenario stamina

> [!WARNING]
> Outdated third-party dumps are not always accurate.
---
# Where Hands-On Experience Is Required

- **IAM and Workload Identity:** Configuring custom roles and resource hierarchies
- **Network Defenses:** Building VPC Service Controls and Cloud Armor policies
- **Encryption (KMS):** Implementing Customer-Managed Encryption Keys (CMEK)
- **Security Operations:** Setting up Security Command Center (SCC) and audit log exports
- **Data Privacy:** Using Cloud DLP to inspect and mask sensitive data
- **GKE Security:** Hardening clusters with RBAC and network policies
---
# Sample 4–6 Week Prep Outline

| Week | Focus |
| :--- | :--- |
| 1 | Exam guide + IAM/hierarchy labs |
| 2 | Network boundary + VPC-SC scenarios |
| 3 | KMS/encryption + data protection |
| 4 | SCC, logging, ops playbooks |
| 5 | Compliance mapping + practice exam |
| 6 | Gap remediation + light review |
---
<!-- layout: 2-column -->
# Exam-Taking Tips

### Reading the Scenario
- Identify the core security requirement first (least privilege, exfiltration prevention, key control, or compliance)
- Eliminate answers that rely on manual toil, primitive roles (`Owner`/`Editor`), or user-managed service account keys
- Watch for qualifiers like *least operational overhead*, *Google-recommended*, or *strict regulatory control*

### Pacing and Strategy
- Budget roughly 2 minutes per question across the 120-minute window
- Flag long multi-service architecture questions, lock in your best answer, and revisit at the end
- Choose native managed Google Cloud controls (VPC-SC, IAP, CMEK, SCC) over custom scripts when both solve the risk
---
# What You Learned

- Described PCSE scope, format, and exam expectations
- Summarized the five core domains and what each tests
- Identified high-yield resources and a practical study path
- Recognized where hands-on Google Cloud experience is required to pass
---
# Quiz 1 of 3

**A financial services team stores sensitive datasets in BigQuery. You must prevent an authorized user, or an attacker using stolen credentials, from copying BigQuery tables to an external Google Cloud project, while allowing queries from corporate networks. What should you configure?**

A. Place the project in a VPC Service Controls perimeter, restrict the `bigquery.googleapis.com` service, and attach an Access Context Manager access level for the corporate IP ranges

B. Remove `roles/bigquery.dataViewer` from all users and grant temporary `roles/owner` access only when queries are needed

C. Configure Cloud NAT and Private Google Access on the VPC subnet

D. Enable BigQuery Data Access audit logs and create a Cloud Monitoring alert when a table copy job completes
---
# Quiz 1: Answer

**A financial services team stores sensitive datasets in BigQuery. You must prevent an authorized user, or an attacker using stolen credentials, from copying BigQuery tables to an external Google Cloud project, while allowing queries from corporate networks. What should you configure?**

**Correct: A.** Place the project in a VPC Service Controls perimeter, restrict the `bigquery.googleapis.com` service, and attach an Access Context Manager access level for the corporate IP ranges

- VPC Service Controls creates a service perimeter around Google Cloud APIs (`bigquery.googleapis.com`) that blocks data movement to unauthorized projects, even with valid IAM credentials
- Access Context Manager access levels permit authorized requests originating from approved corporate IP ranges or device postures
- IAM roles alone (B) cannot stop an authorized user from exporting data to an external project where they hold write permissions
- Audit logs and alerts (D) detect exfiltration after the fact rather than preventing it
---
# Quiz 2 of 3

**Your platform team manages a multi-tenant Google Kubernetes Engine (GKE) cluster. Pods in Namespace A must authenticate to Cloud Storage with their own least-privilege identity, must not communicate with Pods in Namespace B, and must only run container images signed by your CI pipeline. Which combination meets these requirements?**

A. Use the default Compute Engine node service account with `cloud-platform` scope, enable VPC peering, and scan images manually before deployment

B. Enable Workload Identity for GKE, enforce Kubernetes Network Policies between namespaces, and configure Binary Authorization with a required attestor

C. Mount exported service account JSON keys as Kubernetes Secrets, create VPC firewall rules between Pods, and enable Shielded GKE Nodes

D. Grant `cluster-admin` RBAC bindings to each namespace team and enable Container Threat Detection in Security Command Center
---
# Quiz 2: Answer

**Your platform team manages a multi-tenant Google Kubernetes Engine (GKE) cluster. Pods in Namespace A must authenticate to Cloud Storage with their own least-privilege identity, must not communicate with Pods in Namespace B, and must only run container images signed by your CI pipeline. Which combination meets these requirements?**

**Correct: B.** Enable Workload Identity for GKE, enforce Kubernetes Network Policies between namespaces, and configure Binary Authorization with a required attestor

- **Workload Identity for GKE** binds Kubernetes ServiceAccounts to IAM service accounts without node-level credentials or exported JSON keys
- **Kubernetes Network Policies** restrict Pod-to-Pod traffic across namespaces inside the cluster
- **Binary Authorization** enforces deploy-time attestation so only images signed by trusted CI build steps can run
- Node service accounts (A) and mounted JSON keys (C) violate least-privilege keyless design
---
# Quiz 3 of 3

**Security Command Center generates a high-severity finding indicating that a service account’s user-managed key is being used from an unrecognized external IP address to list Cloud Storage buckets. You must contain the incident immediately while preserving evidence for forensic analysis. What should you do first?**

A. Delete the entire Google Cloud project containing the service account and recreate the resources from Terraform

B. Disable or delete the compromised service account key, review Admin Activity and Data Access audit logs for all actions taken by that principal, and transition the workload to keyless authentication

C. Disable Cloud Audit Logs on the project to stop the attacker from generating additional log entries

D. Add `0.0.0.0/0` to a VPC firewall deny rule and leave the service account key active for 30 days
---
# Quiz 3: Answer

**Security Command Center generates a high-severity finding indicating that a service account’s user-managed key is being used from an unrecognized external IP address to list Cloud Storage buckets. You must contain the incident immediately while preserving evidence for forensic analysis. What should you do first?**

**Correct: B.** Disable or delete the compromised service account key, review Admin Activity and Data Access audit logs for all actions taken by that principal, and transition the workload to keyless authentication

- Disabling or revoking the specific compromised key immediately stops unauthorized API calls without destroying forensic project state
- Cloud Audit Logs (Admin Activity and Data Access) establish the blast radius: which buckets or objects were listed or read
- Deleting the project (A) or disabling logs (C) destroys critical forensic evidence
- VPC firewall rules (D) apply to VM network traffic, not direct IAM-authenticated calls to `storage.googleapis.com` from an external IP
---
<!-- layout: title-image -->
# Questions and Answers

![Questions](images/qa.png)
---
<!-- layout: full-bleed -->
# Survey
![ROI Logo](images/hca-2.png)
---
<!-- layout: full-bleed -->
# My Path
![ROI Logo](images/hca-3.png)
---
<!-- layout: full-bleed -->
# Thank You
![ROI Logo](images/hca-4.png)
