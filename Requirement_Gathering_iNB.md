Prompt-1

Act as a Solution Architect.

From this Attached File, list clarification questions a Solution Architect should ask business and product stakeholders before designing a system.

Below is a **structured list of clarification questions** that a **Solution Architect should ask business and product stakeholders**, derived **directly from gaps, assumptions, and ambiguities in the iNB (Indian Net Bank) Case Study** .

I’ve grouped the questions the way they are typically asked in **real architecture discussions**.

**1\. Business Scope & Objectives**

1.  Is this system intended only for **retail customers**, or will it later support **corporate / SME users**?
2.  What are the **business success metrics** for iNB (e.g., active users, transaction volume, cost reduction)?
3.  Is this application meant to **replace existing systems** or **co-exist** with legacy banking platforms?
4.  Are there plans for **future channels** (mobile app, API banking, third-party integrations)?

**2\. User Roles & Access Control**

1.  What user roles exist besides **Customer** (e.g., Banker, Admin, Auditor, Support)?
2.  What actions can **bank staff** perform in the system (approvals, overrides, reports)?
3.  Should customers have **different access levels** based on account type?
4.  Is role-based access control (RBAC) required from day one?

**3\. Customer Registration & Onboarding**

1.  How long does **bank approval** for registration usually take?
2.  Is the approval process **manual or automated**?
3.  Should customers receive **email/SMS notifications** during registration and approval?
4.  Can a customer apply for **multiple accounts** under one login?
5.  Is **KYC verification** (documents, identity proof) required at registration?

**4\. Authentication & Security**

1.  Are **multi-factor authentication (MFA/OTP)** requirements planned beyond username/password?
2.  After account lock (3 invalid attempts), who can unlock it and through which interface?
3.  Are there **password expiry and reset policies**?
4.  Is login activity auditing required (IP, timestamp, device)?
5.  Are there regulatory security standards to comply with (e.g., RBI, PCI-DSS)?

(Only basic lockout rules are defined; advanced security is not specified)

**5\. Accounts & Transactions**

1.  Can a customer hold **both savings and current accounts simultaneously**?
2.  Are **interest rates** configurable via admin UI or static configuration?
3.  How frequently is **interest calculated and credited** for savings accounts?
4.  What is the **daily withdrawal limit**, and who configures it?
5.  Should transaction limits differ by customer type?

**6\. Overdraft & Financial Calculations**

1.  How is overdraft **interest calculated** (formula, rounding rules)?
2.  Is there a **maximum overdraft limit**?
3.  Are customers notified when they enter overdraft?
4.  Are overdraft charges **reversible** under any conditions?
5.  Should overdraft calculations be **real-time or batch-based**?

(The document mentions daily calculation but not implementation specifics)

**7\. Cheque Deposit Workflow**

1.  Is cheque clearance handled **entirely offline**, or does it integrate with clearing systems?
2.  Can a cheque be **cancelled** before being sent for clearance?
3.  What is the **bounce fine amount**, and is it configurable?
4.  Who updates cheque statuses — manually or automatically?
5.  Should customers receive notifications for each status change?

**8\. Bill Payments & Scheduling**

1.  Which **billers** are supported initially?
2.  Is biller integration **manual, API-based, or third-party aggregator**?
3.  Can customers **cancel or modify scheduled payments**?
4.  What happens if **insufficient balance** exists on the scheduled date?
5.  Are payment failures retried automatically?

**9\. Money Transfer**

1.  Can transfers happen only **within iNB**, or also to external banks?
2.  Are transfers **real-time or batch-processed**?
3.  Are transaction limits applied per transfer or per day?
4.  Is transaction confirmation required (OTP)?
5.  Is transaction reversal supported?

**10\. Non-Functional Requirements (NFRs)**

1.  Expected **number of users** and concurrent sessions?
2.  Target **performance SLAs** (login time, transaction time)?
3.  Availability requirements (e.g., 99.9%, 24×7)?
4.  Expected **data retention period** for statements and logs?
5.  Is horizontal scalability required from day one?

(None of these are defined in the case study)

**11\. Reporting & Audit**

1.  Who consumes reconciliation and transaction reports?
2.  Are reports required in **PDF, Excel, or dashboard format**?
3.  How long should audit logs be retained?
4.  Is real-time monitoring required for suspicious activities?

**12\. Deployment & Environment**

1.  Are there **separate environments** (Dev, QA, UAT, Prod)?
2.  Is deployment **on-premises only (IIS)** or cloud-ready?
3.  Are backup, restore, and DR requirements defined?
4.  What is the acceptable **RTO/RPO**?

(IIS deployment is mentioned, but resilience is not)

**13\. Compliance & Legal**

1.  Which **banking regulations** must be followed?
2.  Are there **data privacy** or localization requirements?
3.  Is customer consent tracking required?

Prompt-2

Thinking Mode:

You are a Solution Architect.

From this Attached File, list clarification questions you should ask related to functional and non-functional requirements to your Customer.

**Clarification questions — Functional & Non-Functional (from the iNB case study)**

Below are focused, customer-facing clarification questions I (as the Solution Architect) would ask, organized by area. I pulled these from the iNB case study sections (Customer Registration, Accounts, Cheque Deposits, Bill Payments, Money Transfer, Look-and-feel, Security, Data Fields).

**A. Functional requirements — Customer & Account flows**

**Customer registration & onboarding (Section 2.1)**

1.  Is KYC required at registration (document upload / verification) or only manual bank approval as described? If KYC, which documents and verification rules?
2.  Is the approval step fully manual by bank staff or can parts be automated (e.g., automatic provisional login)?
3.  Should the system support multiple accounts per customer (multiple savings/current accounts) under one customer id?
4.  What notifications are required during onboarding (email, SMS, postal letter mentioned — confirm channels and exact content)?

**Home Page & Statements (Sections 2.2, 2.3)**  
5\. What fields must appear on the post-login home page (summary balance, multiple accounts, alerts)?  
6\. For statements: define exact requirements for the Mini (last 5) and Detailed (date range) statements (PDF export, CSV, pagination).

**Savings & Current account behaviors (Section 2.3.1 / 2.3.2)**  
7\. Who configures: (a) savings interest rate, (b) minimum balance, (c) daily withdrawal limit — and via what UI/role?  
8\. How and when is interest applied to savings accounts (monthly, EOM posting, calculation method)?  
9\. For overdrafts on current accounts: what are eligibility rules, max overdraft per account, and how are limits set?  
10\. Are overdraft charges applied and visible in real-time to the customer, or only in daily batch updates? (Doc says “calculated daily” — confirm implementation expectation).

**Cheque deposit workflow (Section 2.4)**  
11\. Will cheque status changes (Not received → Sent for Clearance → Cleared / Bounced) be driven manually by bank staff or integrated with an external clearing system?  
12\. What data fields are required on the online bank slip? Are scanned images to be stored?  
13\. Define SLA for cheque status updates and whether automatic notifications are required on each status change.  
14\. What is the bounce fine policy (amount, calculation) and reversal/appeal process?

**Bill payments (Section 2.5)**  
15\. Which billers will be supported initially and what integration method: direct API, third-party aggregator, manual entry?  
16\. For scheduled payments: can customers edit/cancel before execution? What is the cutoff time and retry policy on failure?

**Money transfer (Section 2.6)**  
17\. Are transfers limited to internal iNB accounts only, or must we support external bank transfers (NEFT/RTGS/IMPS)?  
18\. What are per-transaction and daily transfer limits? Are these configurable per customer?  
19\. Is OTP/2FA required for transfers and high-value transactions?

**Look-and-feel / Navigation (Section 2.7)**  
20\. Are there branding guidelines, responsive/mobile requirements, and accessibility (WCAG) targets?  
21\. Confirm navigation depth target (“minimum mouse-clicks”) and any required wireframes or example flows.

**Banker / Admin operations**  
22\. What banker roles and permissions are required (view slips, change cheque status, approve registrations, re-activate locked accounts)?  
23\. Which actions must be auditable with user, timestamp and reason (approvals, reversals, manual balance adjustments)?

**Data fields & validation (Section 3.1)**  
24\. Confirm data validation/format rules (username alphabet only, password policy, phone/email formats) and whether these should be enforced client and server side.  
25\. Are there additional customer attributes required (national ID, DOB, tax id) not in the doc?

**B. Non-functional requirements (NFRs)**

**Performance & Scalability**  
26\. Expected total users, daily active users, and peak concurrent sessions? (We need numbers to size app, DB, cache.)  
27\. Target response times for critical flows (login, balance enquiry, transfer) and acceptable percentiles (p95/p99)?  
28\. Expected transaction volume per day (cheques submitted, transfers, bill payments)?

**Availability & SLAs**  
29\. Required availability/uptime (e.g., 99.9% SLA)? Is 24×7 availability required for all services?  
30\. Acceptable maintenance windows and allowable downtime for upgrades?

**Data retention, backup & recovery**  
31\. How long must transactional data, statements, audit logs and cheque records be retained?  
32\. Required RTO (Recovery Time Objective) and RPO (Recovery Point Objective) for production incidents?

**Security & Compliance**  
33\. Confirm regulatory/compliance requirements (RBI, local data residency, PCI-DSS for cards).  
34\. Is encryption required at rest and in transit for all sensitive data? Which encryption standards/policies to apply?  
35\. Do we need MFA, device fingerprinting, session timeouts, and anomaly detection for fraud?  
36\. What is the process for account lock/unlock (the doc says manual re-activation after 3 failed logins) — should support self-service unlock with verification?

**Maintainability & Operability**  
37\. Expected support hours and on-call model for production incidents?  
38\. Monitoring/observability requirements: metrics, alerts, dashboards, and required logging retention?  
39\. Is automated CI/CD and scripted deployment required (the doc mentions IIS deployment — confirm if cloud or containerized deployments are allowed)?

**Interoperability & Integration**  
40\. Which external systems must integrate (core banking, clearing houses, biller networks)? Are standard protocols required (ISO20022, NACHA, REST/SOAP)?

**Usability & Accessibility**  
41\. Any accessibility standards (WCAG) or languages/localization required?  
42\. Mobile support expectations (responsive web vs native mobile apps)?

**Non-functional acceptance criteria**  
43\. How will NFRs be validated for sign-off (load tests, security pen tests, accessibility audit)?

**C. Deliverables & acceptance**

1.  What acceptance criteria does the business expect for each major flow (registration, transfer, cheque deposit, bill pay)?
2.  What are the reporting requirements and sample reports needed for reconciliation (the doc mentions cheque reconciliation)?

Prompt-3

Convert these into a one-page discovery checklist for stakeholder

**✅ Solution Architecture Discovery Checklist**

**Project:** Indian Net Bank (iNB) – Online Banking System  
**Audience:** Business, Product, Operations, Security stakeholders

**1\. Business Scope & Users**

*   ☐ Target users: Retail only or Corporate/SME also?
*   ☐ Channels in scope: Web only now? Mobile / APIs later?
*   ☐ Success metrics (adoption, transactions, cost reduction)?
*   ☐ Co-existence with legacy/core banking systems?

**2\. User Roles & Permissions**

*   ☐ Defined roles: Customer, Banker, Admin, Auditor?
*   ☐ Role-wise permissions clearly defined?
*   ☐ Actions requiring maker–checker approval?
*   ☐ Audit requirements for sensitive actions?

**3\. Customer Registration & Onboarding**

*   ☐ Is KYC required? If yes, which documents?
*   ☐ Approval process: fully manual or partially automated?
*   ☐ Multiple accounts per customer login allowed?
*   ☐ Notifications during onboarding (Email / SMS / Letter)?
*   ☐ Average approval turnaround time?

**4\. Authentication & Security**

*   ☐ Password policy beyond current rules?
*   ☐ MFA / OTP required for login or transactions?
*   ☐ Account lock/unlock workflow (manual vs self-service)?
*   ☐ Session timeout & inactivity rules?
*   ☐ Regulatory security compliance (RBI, PCI, etc.)?

**5\. Accounts & Transactions**

*   ☐ Can customer hold both Savings & Current accounts?
*   ☐ Interest calculation method & frequency (Savings)?
*   ☐ Daily withdrawal limits – configurable by whom?
*   ☐ Minimum balance rules – configurable?
*   ☐ Transaction history export formats (PDF / CSV)?

**6\. Overdraft Management (Current Account)**

*   ☐ Overdraft eligibility criteria?
*   ☐ Maximum overdraft limit per account?
*   ☐ Interest calculation formula & rounding rules?
*   ☐ Real-time vs daily batch overdraft calculation?
*   ☐ Customer alerts for overdraft usage?

**7\. Cheque Deposit Workflow**

*   ☐ Cheque clearance manual or system-integrated?
*   ☐ Required data on online cheque slip?
*   ☐ Status update SLAs?
*   ☐ Bounce fine amount & configuration?
*   ☐ Notification on each status change?
*   ☐ Reconciliation report format & frequency?

**8\. Bill Payments**

*   ☐ Supported billers (utilities, telecom, etc.)?
*   ☐ Integration type (API / aggregator / manual)?
*   ☐ Scheduling rules & cutoff times?
*   ☐ Failure handling & retry logic?
*   ☐ Payment confirmation & receipt requirements?

**9\. Money Transfer**

*   ☐ Internal iNB only or external banks also?
*   ☐ Transfer type: real-time or batch?
*   ☐ Per-transaction & daily limits?
*   ☐ OTP / secondary authentication required?
*   ☐ Reversal & dispute handling?

**10\. Non-Functional Requirements (Critical)**

**Performance & Scale**

*   ☐ Expected total users & concurrent users?
*   ☐ Peak transaction volume per day?
*   ☐ Response time SLAs (login, transfer, statements)?

**Availability & Resilience**

*   ☐ Availability target (e.g., 99.9%)?
*   ☐ Maintenance windows?
*   ☐ RTO / RPO for disaster recovery?

**Security & Compliance**

*   ☐ Encryption at rest & in transit required?
*   ☐ Data retention & archival period?
*   ☐ Fraud monitoring expectations?

**Operations**

*   ☐ Monitoring, logging & alerting expectations?
*   ☐ Support hours & incident escalation?
*   ☐ Deployment model (IIS only, cloud-ready, hybrid)?

**11\. UX, Accessibility & Look-and-Feel**

*   ☐ Branding & UI guidelines?
*   ☐ Accessibility standards (WCAG)?
*   ☐ Mobile responsiveness requirement?
*   ☐ Target clicks per key journey?

**12\. Acceptance & Governance**

*   ☐ Acceptance criteria per major feature?
*   ☐ UAT ownership & sign-off authority?
*   ☐ Reporting & audit deliverables?

Prompt-4

You are a Solution Architect.

From this Attached File, list clarification questions you should ask to Bank Manager.

Questions should be based on High performance, security, and scalability needs.

Below is a **focused set of clarification questions** that I, as a **Solution Architect**, would ask the **Bank Manager**, specifically targeting **High Performance, Security, and Scalability needs**, based on gaps and assumptions in the **iNB Case Study** .

I’ve framed these in **bank-manager language** (business + risk + operations), not technical jargon.

**🔍 Clarification Questions for Bank Manager**

**Context:** iNB Online Banking System  
**Focus:** Performance • Security • Scalability

**1\. High Performance Requirements**

**User Load & Usage Patterns**

1.  How many **total customers** do you expect to use online banking in the first year?
2.  What is the expected **peak concurrent user count**, especially during salary days or bill due dates?
3.  Which activities are **most critical to be fast** (login, balance check, fund transfer, bill payment)?

**Response Time Expectations**

1.  What is the **acceptable response time** for:
    *   Login?
    *   Balance enquiry?
    *   Money transfer confirmation?
2.  During peak hours, is **slower performance acceptable**, or must performance remain consistent?

**Transaction Volume**

1.  Approximate **daily volume** of:
    *   Money transfers?
    *   Bill payments?
    *   Cheque deposits?
2.  Are there known **seasonal or monthly spikes** we should plan for?

**2\. Security Requirements**

**Authentication & Access Control**

1.  Beyond username/password, do you require **OTP or multi-factor authentication** for:
    *   Login?
    *   Money transfers?
    *   Bill payments?
2.  Should different security rules apply to **high-value transactions**?

_(The case study currently mentions only account lock after 3 invalid attempts)_

**Account Lock & Fraud Prevention**

1.  Who is authorized to **unlock a customer account** after lockout?
2.  Should customers be notified immediately if:
    *   Their account is locked?
    *   A failed login attempt occurs?
3.  Do you want **fraud alerts** for unusual activities (multiple failed logins, abnormal transfers)?

**Data Security & Compliance**

1.  Are there **regulatory security standards** we must comply with (e.g., RBI, data privacy laws)?
2.  Should customer data and transactions be **encrypted at rest and in transit**?
3.  Are there **data residency requirements** (data must stay within India)?

**Audit & Traceability**

1.  Do you require **audit logs** for:
    *   Login attempts?
    *   Money transfers?
    *   Cheque status changes?
2.  How long should **audit logs and transaction history** be retained?

**3\. Scalability Requirements**

**Business Growth**

1.  Do you expect **rapid growth** in customers in the next 2–3 years?
2.  Should the system support **future services**, such as:
    *   Mobile banking apps?
    *   External bank transfers?
    *   Corporate banking users?

**Architecture & Deployment**

1.  The case study mentions deployment on **IIS** — should the system be:
    *   On-premise only?
    *   Cloud-ready for future scaling?
2.  Should the system scale **automatically** during high load, or is manual scaling acceptable?

**Availability & Reliability**

1.  What is the **acceptable downtime** for online banking?
2.  Is **24×7 availability** mandatory for all services?
3.  Do you require **disaster recovery** capabilities?
4.  What are acceptable **RTO (recovery time)** and **RPO (data loss tolerance)** values?

**4\. Operational & Reporting Needs**

1.  Do you want **real-time dashboards** showing system health and transaction volumes?
2.  Who should be alerted in case of:
    *   System slowdown?
    *   Security breach?
    *   Service outage?
3.  Are **daily/weekly performance and security reports** required for management review?

**5\. Risk Appetite & Priorities (Very Important)**

1.  What is more critical for the bank:
    *   Maximum security even if it affects usability?
    *   Faster user experience with acceptable risk?
2.  In case of trade-offs, should we prioritize:
    *   Performance
    *   Security
    *   Cost
    *   Speed of delivery?

Prompt-5

You are a Solution Architect.

From this Attached File, list clarification questions you should ask to IT Team of Bank.

Questions should be based on Application and Infrastructure, Data Protection, Identity and Access Management, Network and Security and Compliance, Application Security, Disaster Recovery, Monitoring

Below is a **comprehensive, enterprise-grade set of clarification questions** that I, as a **Solution Architect**, would ask the **Bank’s IT Team**, structured exactly by the areas you requested.  
All questions are **anchored to gaps and assumptions in the iNB Case Study** and aligned with **banking-grade architecture practices** .

**🧩 IT Architecture Clarification Questions**

**Project:** Indian Net Bank (iNB) Online Banking  
**Audience:** Bank IT / Infra / Security Teams

**1️⃣ Application & Infrastructure**

**Application Architecture**

1.  The document mentions transition from **ASP to ASP.NET**—which **.NET version and hosting model** are approved (Framework vs .NET Core/.NET 6+)?
2.  Is the target architecture **monolithic**, **layered**, or **service-oriented** (future microservices readiness)?
3.  Are there any **bank-mandated reference architectures or frameworks** we must follow?
4.  Is the application expected to integrate with an existing **Core Banking System (CBS)** for:
    *   Account balances
    *   Transactions
    *   Interest calculations?

**Infrastructure & Hosting**

1.  The case study specifies **IIS deployment**—is this:
    *   On-premises only?
    *   Private cloud?
    *   Hybrid?
2.  Are multiple **IIS instances** supported behind a load balancer?
3.  Is **containerization** (Docker/Kubernetes) allowed or planned?
4.  What environments are required (Dev, QA, UAT, Prod), and should they be **topology-identical**?

**2️⃣ Data Protection**

**Data Storage & Encryption**

1.  Which **database platform** is approved (SQL Server / Oracle / other)?
2.  Is **encryption at rest** mandatory for:
    *   Customer PII
    *   Transaction data
    *   Audit logs?
3.  What standards are required for **encryption in transit** (TLS version, certificates)?

**Data Lifecycle**

1.  What is the **data retention policy** for:
    *   Transaction history
    *   Cheque deposits
    *   Audit logs?
2.  Is **data masking** required for non-production environments?
3.  Are there **data residency requirements** (data must stay within India)?

**3️⃣ Identity & Access Management (IAM)**

**User Authentication**

1.  Is authentication managed locally or via **central IAM** (LDAP / Active Directory / SSO)?
2.  Beyond username/password, is **MFA/OTP** required for:
    *   Login
    *   Money transfer
    *   Bill payments?

**Authorization & Privileges**

1.  What **roles** are defined for internal users (Banker, Admin, Auditor)?
2.  Is **role-based access control (RBAC)** sufficient or is **attribute-based (ABAC)** required?
3.  Who can manually **unlock customer accounts** after lockout (mentioned in the case study)?

**4️⃣ Network & Security**

**Network Architecture**

1.  Will the application be placed behind:
    *   Firewall
    *   WAF
    *   Reverse proxy?
2.  Are there **network segmentation** rules between:
    *   Web tier
    *   App tier
    *   Database tier?
3.  Are inbound/outbound **IP restrictions** required?

**Threat Protection**

1.  Is DDoS protection required?
2.  Are rate-limiting and bot protection expected at application or gateway level?
3.  Is integration with a **SIEM** platform required?

**5️⃣ Compliance & Regulatory**

1.  Which compliance standards apply:
    *   RBI IT Framework
    *   ISO 27001
    *   PCI-DSS (if applicable)?
2.  Are **periodic audits** (security, access, data) mandatory?
3.  Is **tamper-proof audit logging** required?
4.  Are there regulatory mandates for **logging, monitoring, and reporting**?

**6️⃣ Application Security**

1.  Are secure coding standards (OWASP Top 10) mandatory?
2.  Is **static/dynamic security testing** required in CI/CD?
3.  How are secrets managed (vault, HSM, key management service)?
4.  Are **API security controls** required (OAuth2, JWT, mTLS)?

**7️⃣ Disaster Recovery (DR)**

1.  Is a **DR site** required?
2.  What are the target **RTO and RPO** values?
3.  Should DR be:
    *   Active-passive
    *   Active-active?
4.  How frequently is **DR testing** mandated?

**8️⃣ Monitoring & Observability**

**Monitoring**

1.  What monitoring tools are standard (APM, infra monitoring)?
2.  Are **real-time dashboards** required for:
    *   Transactions
    *   Performance
    *   Security events?

**Logging & Alerting**

1.  Are application logs **centralized**?
2.  Log retention duration?
3.  Alert thresholds for:
    *   Latency
    *   Error rates
    *   Security events?

**9️⃣ Operations & Support**

1.  On-call support model and escalation matrix?
2.  SLAs for incident resolution?
3.  Change management and release approval process?

Prompt-6

You are a Solution Architect.

From this Attached File, list clarification questions you should ask to Security Team Lead of Bank.

Questions should be based on Security, Governance and Compliance and Risk.

Below is a **focused, security-lead–level set of clarification questions** that I, as a **Solution Architect**, would ask the **Security Team Lead of the Bank**, strictly centered on **Security, Governance & Compliance, and Risk**, and grounded in gaps and assumptions from the **iNB Case Study** .

These questions are phrased the way **security reviews and architecture risk assessments** are actually conducted in banks.

**🔐 Clarification Questions for Security Team Lead**

**System:** Indian Net Bank (iNB) – Online Banking  
**Focus:** Security • Governance & Compliance • Risk

**1️⃣ Security Governance & Ownership**

1.  Who is the **security owner** for the iNB application (CISO team, AppSec, InfraSec)?
2.  Is there a **formal security architecture review** required before go-live?
3.  Are there **bank-mandated security standards or baselines** the application must comply with?
4.  Is a **security risk assessment / threat modeling** mandatory for this system?

**2️⃣ Identity, Authentication & Access Control**

1.  The case study defines only username/password and account lock after 3 failures—is this **acceptable for online banking**, or is **MFA mandatory**?
2.  Should MFA be enforced for:
    *   Login
    *   Money transfers
    *   Bill payments
    *   High-value transactions?
3.  What authentication standards are approved (OTP, hardware token, mobile push)?
4.  Are **privileged users** (bank staff/admins) required to use **stronger authentication**?
5.  How is **account lock/unlock** governed, audited, and approved?

**3️⃣ Data Security & Privacy**

1.  What data is classified as **sensitive / confidential / regulated** (PII, balances, transactions)?
2.  Is **encryption at rest** mandatory for:
    *   Customer data
    *   Transaction records
    *   Audit logs?
3.  What encryption standards are approved (AES-256, key rotation policies)?
4.  Are there **data masking or tokenization** requirements for non-production environments?
5.  Are there **data residency or localization** mandates (e.g., India-only storage)?

**4️⃣ Application & API Security**

1.  Are **secure coding standards** (OWASP Top 10) mandatory for this project?
2.  Is **static and dynamic security testing (SAST/DAST)** required before release?
3.  Are APIs required to be secured using **OAuth2, JWT, mTLS**, or bank-specific standards?
4.  Should **rate limiting and anti-automation controls** be enforced for login and transactions?
5.  Are **cheque deposits, bill payments, and transfers** considered high-risk flows requiring extra controls?

**5️⃣ Network Security & Threat Protection**

1.  Is the application required to sit behind a **WAF**?
2.  Are there mandatory **firewall zoning and network segmentation** rules (web/app/db tiers)?
3.  Is **DDoS protection** required for internet-facing banking applications?
4.  Are IP allow-listing or geo-blocking controls required for admin access?

**6️⃣ Logging, Monitoring & Incident Response**

1.  Which security events must be **logged and monitored**:
    *   Failed logins
    *   Account lockouts
    *   Transfers
    *   Cheque status changes?
2.  Is integration with a **SIEM/SOC** mandatory?
3.  What is the **log retention period** for security and audit logs?
4.  Are logs required to be **tamper-proof / write-once**?
5.  What is the **incident response SLA** for:
    *   Security breach
    *   Fraud detection
    *   Data leakage?

**7️⃣ Compliance & Regulatory Requirements**

1.  Which regulatory frameworks apply:
    *   RBI IT / Cyber Security Framework
    *   ISO 27001
    *   PCI-DSS (if payments involved)?
2.  Are **periodic penetration tests** mandatory? If yes, how frequently?
3.  Is a **regulatory audit sign-off** required before production deployment?
4.  Are compliance reports required for:
    *   Access reviews
    *   Transaction monitoring
    *   Security incidents?

**8️⃣ Risk Management & Fraud**

1.  What are the **top security risks** identified for online banking at the bank?
2.  Are there defined **fraud scenarios** we must explicitly design for (credential stuffing, account takeover)?
3.  Should **behavioral or anomaly-based monitoring** be implemented?
4.  What is the **bank’s risk appetite** for:
    *   User convenience vs security
    *   Manual controls vs automation?

**9️⃣ Third-Party & Operational Risk**

1.  Are there **third-party integrations** (billers, clearing houses) that require security assessment?
2.  Is a **vendor risk assessment** mandatory before integration?
3.  Are security clauses required in **SLAs and contracts**?

Prompt-7

You are a Solution Architect.

You have asked hundreds of questions to Customers. Can you share gist of all questions in one page.

Below is a **one-page executive-level gist** of **all the questions** asked across **Customer, Business, IT, Security, and Bank stakeholders**, distilled into **what truly matters for Solution Architecture**.

This is the **cheat sheet** you can use in:

*   Architecture discovery workshops
*   Interviews (Solution Architect / Cloud Architect)
*   Design reviews
*   Client discussions

**🧠 One-Page Solution Architecture Discovery – Gist**

**Context:** Online Banking System (iNB)

**1️⃣ Business & Users (WHY & WHO)**

*   Who are the users (retail, staff, admin)?
*   What business outcomes define success?
*   Expected growth in users and transactions?
*   Future roadmap (mobile, APIs, external banks)?
*   Risk appetite: security vs usability vs cost?

**2️⃣ Functional Scope (WHAT)**

*   Customer onboarding & approval flow?
*   Account types, limits, overdrafts, interest rules?
*   Transfers: internal only or external?
*   Bill payments: instant vs scheduled?
*   Cheque processing: manual vs automated?
*   Required reports, statements, reconciliation?

**3️⃣ Non-Functional Requirements (HOW WELL)**

*   Performance SLAs (login, balance, transfer)?
*   Peak load & concurrency expectations?
*   Availability target (24×7, 99.9%+)?
*   Scalability expectations (today vs 3 years)?
*   Maintenance windows & downtime tolerance?

**4️⃣ Application Architecture**

*   Monolith vs layered vs service-oriented?
*   Technology stack & standards?
*   Integration with core banking systems?
*   Sync vs async processing?
*   Session & state management approach?

**5️⃣ Infrastructure & Deployment**

*   On-prem, cloud, or hybrid?
*   Environments (Dev, QA, UAT, Prod)?
*   Load balancing & high availability?
*   Auto-scaling expectations?
*   CI/CD & release strategy?

**6️⃣ Data & Storage**

*   Database technology & scalability?
*   Data growth & retention policies?
*   Encryption at rest & in transit?
*   Backup, restore, PITR expectations?
*   Data residency & masking needs?

**7️⃣ Identity & Access Management (IAM)**

*   Authentication method (password, OTP, MFA)?
*   Role-based access for users & staff?
*   Privileged access controls?
*   Account lock/unlock governance?
*   Auditability of access?

**8️⃣ Security Controls**

*   Secure coding standards (OWASP)?
*   API security approach?
*   Rate limiting & bot protection?
*   Network security (WAF, firewall, segmentation)?
*   Secrets & key management?

**9️⃣ Compliance & Governance**

*   Regulatory frameworks (RBI, ISO, PCI)?
*   Mandatory audits & approvals?
*   Log retention & tamper-proofing?
*   Pen-testing & security reviews?
*   Documentation & sign-off requirements?

**🔟 Risk & Fraud**

*   Key fraud scenarios to design for?
*   Transaction risk thresholds?
*   Real-time monitoring vs post-facto?
*   Manual vs automated controls?
*   Incident response expectations?

**1️⃣1️⃣ Monitoring & Operations**

*   What to monitor (performance, security, business KPIs)?
*   Alerting & escalation paths?
*   SLA & incident resolution times?
*   Operational dashboards required?

**1️⃣2️⃣ Disaster Recovery & Resilience**

*   DR required or optional?
*   RTO / RPO targets?
*   Active-active vs active-passive?
*   DR testing frequency?