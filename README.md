# CloudMetrics | SOC 2 (Security & Availability) Readiness Assessment

![Framework: AICPA SOC 2](https://img.shields.io/badge/Framework-AICPA%20SOC%202%20(2017%20TSC)-blue.svg?style=flat-square)
[![Trust Services Criteria](https://img.shields.io/badge/Criteria-Security%20(CC)%20%2B%20Availability%20(A1)-0052CC.svg?style=flat-square)](#scoping--system-boundary)
[![Readiness Score](https://img.shields.io/badge/Readiness%20Score-61.4%25%20(In%20Remediation)-f59e0b.svg?style=flat-square)](#readiness-scorecard--gap-summary)
[![Audit Strategy](https://img.shields.io/badge/Strategy-Type%20I%20(M4)%20%E2%86%92%20Type%20II%20(M12)-10b981.svg?style=flat-square)](#remediation-roadmap--audit-strategy)
[![Cloud Infrastructure](https://img.shields.io/badge/Cloud-AWS%20Multi--AZ%20(EKS%20%2B%20RDS)-orange.svg?style=flat-square)](#scoping--system-boundary)

A comprehensive, audit-ready **SOC 2 Type I and Type II Readiness Assessment** for **CloudMetrics**, a fictional high-growth B2B SaaS analytics company (118 employees). 

This project simulates a full-scope GRC engagement conducted by a vCISO / Lead Security & Compliance Consultant. It provides end-to-end audit deliverables: scoping boundaries, asset and vendor inventories, a 5x5 quantitative risk register, an AICPA Trust Services Criteria (TSC) control matrix, a weighted gap assessment with a 12-week remediation roadmap, and an executive summary for executive leadership and the Board of Directors.

---

## Executive Summary & Quick Stats

| Metric | Assessment Result | Notes |
| :--- | :--- | :--- |
| **Target Framework** | AICPA SOC 2 (2017 Trust Services Criteria) | Security (Common Criteria CC1.1–CC9.2) & Availability (A1.1–A1.3) |
| **Total In-Scope Controls** | **35 Controls** (CM-01 through CM-35) | Covering Governance, Access Control, Change Mgmt, SecOps, & BCP/DR |
| **Current Baseline Readiness** | **61.4% Weighted Readiness** | 14 Passed (40.0%), 15 Partial (42.9%), 6 Missing (17.1%) |
| **Top Remediation Targets** | IAM Key Rotation, Pentesting, Offboarding | 3 critical findings blocking enterprise sales cycles |
| **Recommended Audit Path** | **Type I (Month 4) → Type II (Month 12)** | Fast-tracks buyer compliance before starting the 6–12 month observation period |
| **Estimated Year 1 Investment** | **$180,000 – $210,000** | $130,000 core deliverables + $50,000–$80,000 tooling & contingency |

---

## Deliverables & Artifacts Directory

All source deliverables are structured into standardized management memos and analytical workbooks:

| File Name | Deliverable | Format | Description & Contents |
| :--- | :--- | :--- | :--- |
| **[`01_Scoping_Memo.docx`](./01_Scoping_Memo.docx)** | **Scoping & System Boundary Memo** | Word (.docx) | Formal definition of audit boundary, included AWS accounts/services, SaaS tools, excluded corporate functions, and Type I vs. Type II strategy. |
| **[`02_Asset_and_Vendor_Inventory.xlsx`](./02_Asset_and_Vendor_Inventory.xlsx)** | **Asset & Vendor Inventory** | Excel (.xlsx) | Dual-sheet inventory tracking **12 core system assets** (EKS, RDS, S3, Okta, Datadog) and **10 third-party vendors** with data classification, tiering, and SOC 2 / Bridge letter review dates. |
| **[`03_Risk_Register.xlsx`](./03_Risk_Register.xlsx)** | **Quantitative Risk Register** | Excel (.xlsx) | **15 prioritized risks** evaluated on a 5×5 Likelihood × Impact matrix, mapped to control owners, treatment strategies (Mitigate vs. Accept), and residual risk sign-off protocols. |
| **[`04_Control_Matrix.xlsx`](./04_Control_Matrix.xlsx)** | **SOC 2 Control Matrix** | Excel (.xlsx) | **35 detailed controls** mapped to AICPA 2017 Trust Services Criteria (CC1.1–CC9.2, A1.1–A1.3), control nature (Preventive/Detective), frequencies, and verifiable audit evidence sources. |
| **[`05_Gap_Assessment_and_Roadmap.xlsx`](./05_Gap_Assessment_and_Roadmap.xlsx)** | **Gap Assessment & Remediation Roadmap** | Excel (.xlsx) | Tri-tab workbook containing: <br>• **Gap Assessment**: Control-by-control gap evaluation (PASS/PARTIAL/MISSING)<br>• **Roadmap**: 3-phase remediation plan (Quick Wins, Core Controls, Mature & Operate)<br>• **Summary**: Dynamic statistical scoreboard with weighted formulas. |
| **[`08_Executive_Summary.docx`](./08_Executive_Summary.docx)** | **Executive & Board Summary** | Word (.docx) | C-suite decision brief detailing bottom-line readiness (61%), top 3 deal-breaker risks, detailed year-one resource/budget ask, and go-to-market rollout advice. |

---

## Scoping & System Boundary

### In-Scope vs. Out-of-Scope Matrix

```
                      +-----------------------------------------------------------+
                      |                 CloudMetrics SOC 2 Boundary               |
                      |                                                           |
                      |   +--------------------+       +----------------------+   |
                      |   | AWS Infrastructure |       | Admin & Identity     |   |
                      |   | - us-east-1 (Prod) | <===> | - Okta Workforce IdP |   |
                      |   | - us-west-2 (DR)   |       | - GitHub CI/CD & ECR |   |
                      |   | - EKS Node.js API  |       | - Atlassian Jira     |   |
                      |   | - Multi-AZ RDS PG  |       | - Datadog Monitoring |   |
                      |   | - Customer S3      |       | - CloudTrail Archive |   |
                      |   +--------------------+       +----------------------+   |
                      |              ^                             ^              |
                      |              |                             |              |
                      |              v                             v              |
                      |   +---------------------------------------------------+   |
                      |   | In-Scope Customer Data Subservice Vendors         |   |
                      |   | - Stripe (Billing)          - Cloudflare (WAF/CDN)|   |
                      |   | - Twilio SendGrid (Email)   - Sentry (Error APM)  |   |
                      |   +---------------------------------------------------+   |
                      +-----------------------------------------------------------+
                                                    |
                                       [ EXCLUDED / OUT OF SCOPE ]
                                                    v
                      +-----------------------------------------------------------+
                      | - Marketing Web Server (HostGator - static, no PII)      |
                      | - HR Management & Payroll (Gusto)                         |
                      | - Internal Corporate Laptops without Production Access     |
                      | - Trust Criteria: Processing Integrity, Confidentiality,  |
                      |   and Privacy (Deferred to Cycle 2 upon buyer demand)     |
                      +-----------------------------------------------------------+
```

* **Trust Services Criteria (TSC) Included**:
  * **Security (Common Criteria CC1.1 – CC9.2)**: Firewalls, IAM, encryption at rest/transit, vulnerability management, incident response, physical/logical access.
  * **Availability (A1.1 – A1.3)**: System resilience, multi-AZ failover, daily automated backups, cross-region restore testing, and capacity planning.
* **Core Systems**:
  * `AST-01` to `AST-05`: Production AWS Account (`prod-cm-app` in `us-east-1` primary, `us-west-2` DR), Amazon EKS cluster (`cm-prod-eks`), Amazon RDS PostgreSQL 15 (Multi-AZ), and Customer Uploads S3 bucket.
  * `AST-06` to `AST-12`: Okta Workforce Tenant, GitHub Enterprise, Jira Service Management, Datadog US1, CloudTrail dedicated security log archive, CI/CD ECR, and AWS KMS/Secrets Manager.

---

## Readiness Scorecard & Gap Summary

The readiness evaluation scores controls based on auditor evidentiary standards: **PASS** (1.0 weight - fully implemented and evidenced), **PARTIAL** (0.5 weight - active practice but missing formal documentation or consistent proof), and **MISSING** (0.0 weight - control absent).

### Overall Readiness Breakdown

```
  [####################                    ] 61.4%
  Passed: 14 (40.0%) | Partial: 15 (42.9%) | Missing: 6 (17.1%) | Total Controls: 35
```

| Status | Count | Share | Weighted Contribution | Key Included Controls |
| :--- | :---: | :---: | :---: | :--- |
| **PASS** | **14** | 40.0% | 14.0 | CM-01 (AUP/Conduct), CM-03 (Background checks), CM-08 (MFA on all logins), CM-09 (RBAC), CM-13 (KMS Encryption at rest), CM-14 (TLS 1.3 in transit), CM-15 (WAF & Security Groups), CM-16 (GuardDuty enabled), CM-18 (Vulnerability scanning), CM-20 (Secrets Manager), CM-22 (IR plan documented), CM-27 (Git feature branch PRs), CM-29 (Multi-AZ RDS), CM-34 (Datadog monitors). |
| **PARTIAL** | **15** | 42.9% | 7.5 | CM-02 (Policy reviews), CM-04 (Quarterly self-assessments), CM-05 (RACI documentation), CM-07 (Policy exceptions), CM-10 (Quarterly access reviews), CM-11 (Deprovisioning SLA), CM-12 (IAM key rotation), CM-19 (Endpoint MDM/EDR), CM-21 (On-call alerting), CM-25 (Incident severity matrix), CM-26 (Post-mortems), CM-28 (Prod deploy approvals), CM-30 (Cross-region DR testing), CM-31 (Vendor review tracking), CM-33 (Capacity alerts). |
| **MISSING** | **6** | 17.1% | 0.0 | CM-06 (Formal risk assessment workshop), CM-17 (PostgreSQL `pgaudit` logging), CM-23 (Independent 3rd-party penetration test), CM-24 (Annual incident tabletop simulation), CM-32 (Standard vendor security questionnaire), CM-35 (RTO/RPO SLA definitions). |
| **Total** | **35** | **100%** | **21.5 / 35.0** | **Weighted Readiness: 61.4%** |

---

## Top Risks & Treatment Plan

Extracted from [`03_Risk_Register.xlsx`](./03_Risk_Register.xlsx), scored on a 5×5 Likelihood × Impact scale (1–25):

| Risk ID | Score | Risk Title & Scenario | Treatment | Required Remediation Action |
| :---: | :---: | :--- | :---: | :--- |
| **R-01** | **20** (L4×I5) | **Long-lived IAM access keys exposed**<br>Two production IAM keys >300 days old. Exposure in laptops/logs allows direct AWS account compromise. | Mitigate | Revoke permanent human keys; implement AWS IAM Identity Center (SSO) and AWS Organizations SCP blocking long-lived keys. |
| **R-02** | **16** (L4×I4) | **Exploitable flaws in customer application**<br>No independent external penetration test has ever been conducted on the API or React web app. | Mitigate | Procure third-party CREST/OSCP-accredited penetration test ($15,000); remediate high/critical findings prior to Type I audit date. |
| **R-03** | **15** (L3×I5) | **Departing employees retain system access**<br>Offboarding takes up to 3 days manually; GitHub/Datadog accounts remain unlinked to Okta deactivation. | Mitigate | Deploy Okta SCIM automated provisioning/deprovisioning across GitHub and Datadog; establish mandatory HR-to-IT same-day webhook. |
| **R-04** | **15** (L3×I5) | **Unmonitored privileged database queries**<br>Engineers access production PostgreSQL without query-level logging; `pgaudit` is disabled. | Mitigate | Enable AWS RDS `pgaudit` extension, stream privileged DDL/DML logs to CloudWatch/Datadog, and establish weekly review sign-offs. |
| **R-14** | **6** (L2×I3) | **Datadog platform outage delays security alerts**<br>Centralized monitoring dependency; full secondary redundancy costs $40k/yr (not economically justified). | **Accept (Exec)** | **Residual Risk Accepted**: CloudTrail & GuardDuty write independently to isolated S3 archive. Requires signed CEO/CFO risk acceptance form. |

---

## Remediation Roadmap & Audit Strategy

The 12-week roadmap is partitioned into three phases designed to eliminate enterprise deal-breakers immediately while preparing institutional evidence:

```
[Month 1] Phase 1: Quick Wins (Weeks 1-4)
    ├── Revoke long-lived IAM keys & apply SCP (CM-12)
    ├── Enforce 2-person peer review on GitHub prod deploys (CM-28)
    ├── Approve formal Information Security Policies & Exception process (CM-02, CM-07)
    ├── Implement Okta SCIM leaver sync for GitHub & Datadog (CM-11)
    └── Request vendor SOC 2 reports & bridge letters (CM-31)

[Month 2-3] Phase 2: Core Controls (Weeks 5-12)
    ├── Complete first formal quarterly access review with manager sign-off (CM-10)
    ├── Enable RDS PostgreSQL pgaudit & privileged session reviews (CM-17)
    ├── Roll out MDM disk encryption & EDR agents to engineering laptops (CM-19)
    ├── Conduct external network & application penetration test (CM-23)
    ├── Run annual Ransomware / Breach incident response tabletop simulation (CM-24)
    ├── Execute quarterly database point-in-time restore into us-west-2 (CM-30)
    └── Execute formal Risk Assessment Workshop & Datadog sign-off (CM-06, CM-04)

[Month 4] ---> SOC 2 TYPE I AUDIT EXAMINATION
    └── Independent CPA firm evaluates control design as of a specific point in time.
    └── Unblocks enterprise RFP security questionnaires and vendor diligence.

[Month 5-12] Phase 3: Mature & Operate (Observation Period)
    ├── Continuous automated evidence gathering via compliance automation platform
    ├── Recurring quarterly access reviews and vendor risk evaluations
    └── ---> SOC 2 TYPE II AUDIT REPORT (Testing operating effectiveness over 6-12 months)
```

---

## Resource Requirements & Year 1 Budget

| Investment Category | Scope & Purpose | Estimated Cost |
| :--- | :--- | :---: |
| **Fractional CISO (vCISO)** | 12-month advisory, policy authoring, audit representation, and risk management | $60,000 |
| **External Penetration Testing** | Grey-box web application and cloud infrastructure penetration test | $15,000 |
| **Compliance Automation Platform** | Automated evidence collection, API monitoring, and vendor tracking (e.g. Vanta / Drata) | $25,000 |
| **SOC 2 Type I Audit Fee** | Licensed CPA firm examination fee (Type I attestation report) | $30,000 |
| **Tooling Upgrades & Licenses** | MDM licenses (Kandji/Jamf), EDR agent licensing, PagerDuty on-call, Okta SCIM tier | $30,000 – $50,000 |
| **Remediation Contingency** | External engineering support, cloud architectural tweaks, or specialized legal counsel | $20,000 – $30,000 |
| **Total Year 1 Readiness Budget** | **Complete Readiness through Type I Attestation** | **$180,000 – $210,000** |
| *Year 2 Type II Audit Fee* | *Subsequent 12-month operational effectiveness examination* | *~$50,000* |

---

## Repository Structure

```
cloudmetrics-soc2-readiness/
├── .gitignore                          # Standard gitignore (Office locks, temp files)
├── README.md                           # Master repository documentation & GRC briefing
├── 01_Scoping_Memo.docx                # Scoping memo & system boundary definition
├── 02_Asset_and_Vendor_Inventory.xlsx  # 12 Assets & 10 Vendors classified by risk tier
├── 03_Risk_Register.xlsx               # 15 Risks mapped to 5x5 matrix & remediation actions
├── 04_Control_Matrix.xlsx              # 35 Controls mapped to AICPA 2017 TSC criteria
├── 05_Gap_Assessment_and_Roadmap.xlsx  # Gap assessment, 12-week roadmap, & summary scoreboard
└── 08_Executive_Summary.docx           # Executive leadership decision memo & budget plan
```

---

## Compliance & Evaluation Standards

This project adheres to the following professional audit and security frameworks:
* **AICPA TSP Section 100**: 2017 Trust Services Criteria for Security, Availability, Processing Integrity, Confidentiality, and Privacy.
* **NIST SP 800-53 Rev. 5**: Recommended security and privacy controls for information systems and organizations.
* **AWS Shared Responsibility Model**: Delineating customer configuration responsibilities from AWS hypervisor/physical data center guarantees.
* **Center for Internet Security (CIS) AWS Foundations Benchmark v2.0**: Cloud security baseline controls.

---

## Author & Project Credits

* **Author**: Sagar Chhetri ([@Sagarchhetri83](https://github.com/Sagarchhetri83))
* **Domain**: Information Security, IT Audit, Governance, Risk & Compliance (GRC)
* **Context**: Mock SOC 2 Readiness Engagement simulating real-world B2B SaaS security engineering & audit readiness.
