Requirements gathering for business and product stakeholders.
1. Business Scope & Objectives
1.	Is this system intended only for retail customers, or will it later support corporate / SME users?
2.	What are the business success metrics for iNB (e.g., active users, transaction volume, cost reduction)?
3.	Is this application meant to replace existing systems or co-exist with legacy banking platforms?
4.	Are there plans for future channels (mobile app, API banking, third-party integrations)?
________________________________________
2. User Roles & Access Control
1.	What user roles exist besides Customer (e.g., Banker, Admin, Auditor, Support)?
2.	What actions can bank staff perform in the system (approvals, overrides, reports)?
3.	Should customers have different access levels based on account type?
4.	Is role-based access control (RBAC) required from day one?
________________________________________
3. Customer Registration & Onboarding
1.	How long does bank approval for registration usually take?
2.	Is the approval process manual or automated?
3.	Should customers receive email/SMS notifications during registration and approval?
4.	Can a customer apply for multiple accounts under one login?
5.	Is KYC verification (documents, identity proof) required at registration?
________________________________________
4. Authentication & Security
1.	Are multi-factor authentication (MFA/OTP) requirements planned beyond username/password?
2.	After account lock (3 invalid attempts), who can unlock it and through which interface?
3.	Are there password expiry and reset policies?
4.	Is login activity auditing required (IP, timestamp, device)?
5.	Are there regulatory security standards to comply with (e.g., RBI, PCI-DSS)?
________________________________________
5. Accounts & Transactions
1.	Can a customer hold both savings and current accounts simultaneously?
2.	Are interest rates configurable via admin UI or static configuration?
3.	How frequently is interest calculated and credited for savings accounts?
4.	What is the daily withdrawal limit, and who configures it?
5.	Should transaction limits differ by customer type?
________________________________________
6. Overdraft & Financial Calculations
1.	How is overdraft interest calculated (formula, rounding rules)?
2.	Is there a maximum overdraft limit?
3.	Are customers notified when they enter overdraft?
4.	Are overdraft charges reversible under any conditions?
5.	Should overdraft calculations be real-time or batch-based?
________________________________________
7. Cheque Deposit Workflow
1.	Is cheque clearance handled entirely offline, or does it integrate with clearing systems?
2.	Can a cheque be cancelled before being sent for clearance?
3.	What is the bounce fine amount, and is it configurable?
4.	Who updates cheque statuses — manually or automatically?
5.	Should customers receive notifications for each status change?
________________________________________
8. Bill Payments & Scheduling
1.	Which billers are supported initially?
2.	Is biller integration manual, API-based, or third-party aggregator?
3.	Can customers cancel or modify scheduled payments?
4.	What happens if insufficient balance exists on the scheduled date?
5.	Are payment failures retried automatically?
________________________________________
9. Money Transfer
1.	Can transfers happen only within iNB, or also to external banks?
2.	Are transfers real-time or batch-processed?
3.	Are transaction limits applied per transfer or per day?
4.	Is transaction confirmation required (OTP)?
5.	Is transaction reversal supported?
________________________________________
10. Non-Functional Requirements (NFRs)
1.	Expected number of users and concurrent sessions?
2.	Target performance SLAs (login time, transaction time)?
3.	Availability requirements (e.g., 99.9%, 24×7)?
4.	Expected data retention period for statements and logs?
5.	Is horizontal scalability required from day one?
________________________________________
11. Reporting & Audit
1.	Who consumes reconciliation and transaction reports?
2.	Are reports required in PDF, Excel, or dashboard format?
3.	How long should audit logs be retained?
4.	Is real-time monitoring required for suspicious activities?
________________________________________
12. Deployment & Environment
1.	Are there separate environments (Dev, QA, UAT, Prod)?
2.	Is deployment on-premises only (IIS) or cloud-ready?
3.	Are backup, restore, and DR requirements defined?
4.	What is the acceptable RTO/RPO?
________________________________________
13. Compliance & Legal
1.	Which banking regulations must be followed?
2.	Are there data privacy or localization requirements?
3.	Is customer consent tracking required?
________________________________________
 
Requirements gathering Regarding Functional & Non-Functional.

A. Functional requirements — Customer & Account flows
Customer registration & onboarding:
1.	Is KYC required at registration (document upload / verification) or only manual bank approval as described? If KYC, which documents and verification rules?
2.	Is the approval step fully manual by bank staff or can parts be automated (e.g., automatic provisional login)?
3.	Should the system support multiple accounts per customer (multiple savings/current accounts) under one customer id?
4.	What notifications are required during onboarding (email, SMS, postal letter mentioned — confirm channels and exact content)?
Home Page & Statements:
5. What fields must appear on the post-login home page (summary balance, multiple accounts, alerts)?
6. For statements: define exact requirements for the Mini (last 5) and Detailed (date range) statements (PDF export, CSV, pagination).
Savings & Current account Behaviors: 
7. Who configures: (a) savings interest rate, (b) minimum balance, (c) daily withdrawal limit — and via what UI/role?
8. How and when is interest applied to savings accounts (monthly, EOM posting, calculation method)?
9. For overdrafts on current accounts: what are eligibility rules, max overdraft per account, and how are limits set?
10. Are overdraft charges applied and visible in real-time to the customer, or only in daily batch updates? 
Cheque deposit workflow :
11. Will cheque status changes (Not received → Sent for Clearance → Cleared / Bounced) be driven manually by bank staff or integrated with an external clearing system?
12. What data fields are required on the online bank slip? Are scanned images to be stored?
13. Define SLA for cheque status updates and whether automatic notifications are required on each status change.
14. What is the bounce fine policy (amount, calculation) and reversal/appeal process?
Bill payments :
15. Which billers will be supported initially and what integration method: direct API, third-party aggregator, manual entry?
16. For scheduled payments: can customers edit/cancel before execution? What is the cutoff time and retry policy on failure?
Money transfer :
17. Are transfers limited to internal iNB accounts only, or must we support external bank transfers (NEFT/RTGS/IMPS)?
18. What are per-transaction and daily transfer limits? Are these configurable per customer?
19. Is OTP/2FA required for transfers and high-value transactions?
Look-and-feel / Navigation :
20. Are there branding guidelines, responsive/mobile requirements, and accessibility (WCAG) targets?
21. Confirm navigation depth target (“minimum mouse-clicks”) and any required wireframes or example flows.
Banker / Admin operations:
22. What banker roles and permissions are required (view slips, change cheque status, approve registrations, re-activate locked accounts)?
23. Which actions must be auditable with user, timestamp and reason (approvals, reversals, manual balance adjustments)?
Data fields & validation:
24. Confirm data validation/format rules (username alphabet only, password policy, phone/email formats) and whether these should be enforced client and server side.
25. Are there additional customer attributes required (national ID, DOB, tax id) not in the doc?
________________________________________
B. Non-functional requirements
Performance & Scalability:
26. Expected total users, daily active users, and peak concurrent sessions? (We need numbers to size app, DB, cache.)
27. Target response times for critical flows (login, balance enquiry, transfer) and acceptable percentiles (p95/p99)?
28. Expected transaction volume per day (cheques submitted, transfers, bill payments)?
Availability & SLAs:
29. Required availability/uptime (e.g., 99.9% SLA)? Is 24×7 availability required for all services?
30. Acceptable maintenance windows and allowable downtime for upgrades?
Data retention, backup & recovery:
31. How long must transactional data, statements, audit logs and cheque records be retained?
32. Required RTO (Recovery Time Objective) and RPO (Recovery Point Objective) for production incidents?
Security & Compliance:
33. Confirm regulatory/compliance requirements (RBI, local data residency, PCI-DSS for cards).
34. Is encryption required at rest and in transit for all sensitive data? Which encryption standards/policies to apply?
35. Do we need MFA, device fingerprinting, session timeouts, and anomaly detection for fraud?
36. What is the process for account lock/unlock (the doc says manual re-activation after 3 failed logins) — should support self-service unlock with verification?
Maintainability & Operability:
37. Expected support hours and on-call model for production incidents?
38. Monitoring/observability requirements: metrics, alerts, dashboards, and required logging retention?
39. Is automated CI/CD and scripted deployment required (the doc mentions IIS deployment — confirm if cloud or containerized deployments are allowed)?
Interoperability & Integration:
40. Which external systems must integrate (core banking, clearing houses, biller networks)? Are standard protocols required (ISO20022, NACHA, REST/SOAP)?
Usability & Accessibility:
41. Any accessibility standards (WCAG) or languages/localization required?
42. Mobile support expectations (responsive web vs native mobile apps)?
Non-functional acceptance criteria:
43. How will NFRs be validated for sign-off (load tests, security pen tests, accessibility audit)?
________________________________________
C. Deliverables & acceptance
44.	What acceptance criteria does the business expect for each major flow (registration, transfer, cheque deposit, bill pay)?
45.	What are the reporting requirements and sample reports needed for reconciliation (the doc mentions cheque reconciliation)?
________________________________________
 
Requirements gathering for Bank Manager. The questions are based on High performance, security, and scalability needs.
1. High Performance Requirements
User Load & Usage Patterns:
1.	How many total customers do you expect to use online banking in the first year?
2.	What is the expected peak concurrent user count, especially during salary days or bill due dates?
3.	Which activities are most critical to be fast (login, balance check, fund transfer, bill payment)?
Response Time Expectations:
4.	What is the acceptable response time for:
o	Login?
o	Balance enquiry?
o	Money transfer confirmation?
5.	During peak hours, is slower performance acceptable, or must performance remain consistent?
Transaction Volume:
6.	Approximate daily volume of:
o	Money transfers?
o	Bill payments?
o	Cheque deposits?
7.	Are there known seasonal or monthly spikes we should plan for?
________________________________________
2. Security Requirements
Authentication & Access Control:
8.	Beyond username/password, do you require OTP or multi-factor authentication for:
o	Login?
o	Money transfers?
o	Bill payments?
9.	Should different security rules apply to high-value transactions?
________________________________________

Account Lock & Fraud Prevention:
10.	Who is authorized to unlock a customer account after lockout?
11.	Should customers be notified immediately if:
o	Their account is locked?
o	A failed login attempt occurs?
12.	Do you want fraud alerts for unusual activities (multiple failed logins, abnormal transfers)?
________________________________________
Data Security & Compliance:
13.	Are there regulatory security standards we must comply with (e.g., RBI, data privacy laws)?
14.	Should customer data and transactions be encrypted at rest and in transit?
15.	Are there data residency requirements (data must stay within India)?
________________________________________
Audit & Traceability:
16.	Do you require audit logs for:
o	Login attempts?
o	Money transfers?
o	Cheque status changes?
17.	How long should audit logs and transaction history be retained?
________________________________________
3. Scalability Requirements
Business Growth:
18.	Do you expect rapid growth in customers in the next 2–3 years?
19.	Should the system support future services, such as:
o	Mobile banking apps?
o	External bank transfers?
o	Corporate banking users?
________________________________________
Architecture & Deployment:
20.	The case study mentions deployment on IIS — should the system be:
o	On-premise only?
o	Cloud-ready for future scaling?
21.	Should the system scale automatically during high load, or is manual scaling acceptable?
________________________________________
Availability & Reliability:
22.	What is the acceptable downtime for online banking?
23.	Is 24×7 availability mandatory for all services?
24.	Do you require disaster recovery capabilities?
25.	What are acceptable RTO (recovery time) and RPO (data loss tolerance) values?
________________________________________
4. Operational & Reporting Needs:
26.	Do you want real-time dashboards showing system health and transaction volumes?
27.	Who should be alerted in case of:
o	System slowdown?
o	Security breach?
o	Service outage?
28.	Are daily/weekly performance and security reports required for management review?
________________________________________
5. Risk Appetite & Priorities (Very Important):
29.	What is more critical for the bank:
o	Maximum security even if it affects usability?
o	Faster user experience with acceptable risk?
30.	In case of trade-offs, should we prioritize:
o	Performance
o	Security
o	Cost
o	Speed of delivery?
________________________________________
 

Requirements gathering for IT Team Leads. The questions are based on Application and Infrastructure, Data Protection, Identity and Access Management, Network and Security and Compliance, Application Security, Disaster Recovery, Monitoring 
1️⃣ Application & Infrastructure
Application Architecture:
1.	The document mentions transition from ASP to ASP.NET—which .NET version and hosting model are approved (Framework vs .NET Core/.NET 6+)?
2.	Is the target architecture monolithic, layered, or service-oriented (future microservices readiness)?
3.	Are there any bank-mandated reference architectures or frameworks we must follow?
4.	Is the application expected to integrate with an existing Core Banking System (CBS) for:
o	Account balances
o	Transactions
o	Interest calculations?
________________________________________
Infrastructure & Hosting:
5.	The case study specifies IIS deployment—is this:
o	On-premises only?
o	Private cloud?
o	Hybrid?
6.	Are multiple IIS instances supported behind a load balancer?
7.	Is containerization (Docker/Kubernetes) allowed or planned?
8.	What environments are required (Dev, QA, UAT, Prod), and should they be topology-identical?
________________________________________
2️⃣ Data Protection
Data Storage & Encryption:
9.	Which database platform is approved (SQL Server / Oracle / other)?
10.	Is encryption at rest mandatory for:
o	Customer PII
o	Transaction data
o	Audit logs?
11.	What standards are required for encryption in transit (TLS version, certificates)?
________________________________________
Data Lifecycle:
12.	What is the data retention policy for:
o	Transaction history
o	Cheque deposits
o	Audit logs?
13.	Is data masking required for non-production environments?
14.	Are there data residency requirements (data must stay within India)?
________________________________________
3️⃣ Identity & Access Management (IAM)
User Authentication:
15.	Is authentication managed locally or via central IAM (LDAP / Active Directory / SSO)?
16.	Beyond username/password, is MFA/OTP required for:
o	Login
o	Money transfer
o	Bill payments?
________________________________________
Authorization & Privileges:
17.	What roles are defined for internal users (Banker, Admin, Auditor)?
18.	Is role-based access control (RBAC) sufficient or is attribute-based (ABAC) required?
19.	Who can manually unlock customer accounts after lockout (mentioned in the case study)?
________________________________________
4️⃣ Network & Security
Network Architecture:
20.	Will the application be placed behind:
o	Firewall
o	WAF
o	Reverse proxy?
21.	Are there network segmentation rules between:
o	Web tier
o	App tier
o	Database tier?
22.	Are inbound/outbound IP restrictions required?
________________________________________
Threat Protection:
23.	Is DDoS protection required?
24.	Are rate-limiting and bot protection expected at application or gateway level?
25.	Is integration with a SIEM platform required?
________________________________________
5️⃣ Compliance & Regulatory
26.	Which compliance standards apply:
o	RBI IT Framework
o	ISO 27001
o	PCI-DSS (if applicable)?
27.	Are periodic audits (security, access, data) mandatory?
28.	Is tamper-proof audit logging required?
29.	Are there regulatory mandates for logging, monitoring, and reporting?
________________________________________
6️⃣ Application Security
30.	Are secure coding standards (OWASP Top 10) mandatory?
31.	Is static/dynamic security testing required in CI/CD?
32.	How are secrets managed (vault, HSM, key management service)?
33.	Are API security controls required (OAuth2, JWT, mTLS)?
________________________________________
7️⃣ Disaster Recovery (DR)
34.	Is a DR site required?
35.	What are the target RTO and RPO values?
36.	Should DR be:
o	Active-passive
o	Active-active?
37.	How frequently is DR testing mandated?
________________________________________
8️⃣ Monitoring & Observability
Monitoring
38.	What monitoring tools are standard (APM, infra monitoring)?
39.	Are real-time dashboards required for:
o	Transactions
o	Performance
o	Security events?
________________________________________
Logging & Alerting
40.	Are application logs centralized?
41.	Log retention duration?
42.	Alert thresholds for:
o	Latency
o	Error rates
o	Security events?
________________________________________
9️⃣ Operations & Support
43.	On-call support model and escalation matrix?
44.	SLAs for incident resolution?
45.	Change management and release approval process?









Requirements gathering for Security Team Leads. The questions are based on Security, Governance and Compliance and Risk
1️⃣ Security Governance & Ownership
1.	Who is the security owner for the iNB application (CISO team, AppSec, InfraSec)?
2.	Is there a formal security architecture review required before go-live?
3.	Are there bank-mandated security standards or baselines the application must comply with?
4.	Is a security risk assessment / threat modeling mandatory for this system?
________________________________________
2️⃣ Identity, Authentication & Access Control
5.	The case study defines only username/password and account lock after 3 failures—is this acceptable for online banking, or is MFA mandatory?
6.	Should MFA be enforced for:
o	Login
o	Money transfers
o	Bill payments
o	High-value transactions?
7.	What authentication standards are approved (OTP, hardware token, mobile push)?
8.	Are privileged users (bank staff/admins) required to use stronger authentication?
9.	How is account lock/unlock governed, audited, and approved?
________________________________________
3️⃣ Data Security & Privacy
10.	What data is classified as sensitive / confidential / regulated (PII, balances, transactions)?
11.	Is encryption at rest mandatory for:
o	Customer data
o	Transaction records
o	Audit logs?
12.	What encryption standards are approved (AES-256, key rotation policies)?
13.	Are there data masking or tokenization requirements for non-production environments?
14.	Are there data residency or localization mandates (e.g., India-only storage)?
________________________________________

4️⃣ Application & API Security
15.	Are secure coding standards (OWASP Top 10) mandatory for this project?
16.	Is static and dynamic security testing (SAST/DAST) required before release?
17.	Are APIs required to be secured using OAuth2, JWT, mTLS, or bank-specific standards?
18.	Should rate limiting and anti-automation controls be enforced for login and transactions?
19.	Are cheque deposits, bill payments, and transfers considered high-risk flows requiring extra controls?
________________________________________
5️⃣ Network Security & Threat Protection
20.	Is the application required to sit behind a WAF?
21.	Are there mandatory firewall zoning and network segmentation rules (web/app/db tiers)?
22.	Is DDoS protection required for internet-facing banking applications?
23.	Are IP allow-listing or geo-blocking controls required for admin access?
________________________________________
6️⃣ Logging, Monitoring & Incident Response
24.	Which security events must be logged and monitored:
o	Failed logins
o	Account lockouts
o	Transfers
o	Cheque status changes?
25.	Is integration with a SIEM/SOC mandatory?
26.	What is the log retention period for security and audit logs?
27.	Are logs required to be tamper-proof / write-once?
28.	What is the incident response SLA for:
o	Security breach
o	Fraud detection
o	Data leakage?
________________________________________
7️⃣ Compliance & Regulatory Requirements
29.	Which regulatory frameworks apply:
o	RBI IT / Cyber Security Framework
o	ISO 27001
o	PCI-DSS (if payments involved)?
30.	Are periodic penetration tests mandatory? If yes, how frequently?
31.	Is a regulatory audit sign-off required before production deployment?
32.	Are compliance reports required for:
o	Access reviews
o	Transaction monitoring
o	Security incidents?
________________________________________
8️⃣ Risk Management & Fraud
33.	What are the top security risks identified for online banking at the bank?
34.	Are there defined fraud scenarios we must explicitly design for (credential stuffing, account takeover)?
35.	Should behavioral or anomaly-based monitoring be implemented?
36.	What is the bank’s risk appetite for:
o	User convenience vs security
o	Manual controls vs automation?
________________________________________
9️⃣ Third-Party & Operational Risk
37.	Are there third-party integrations (billers, clearing houses) that require security assessment?
38.	Is a vendor risk assessment mandatory before integration?
39.	Are security clauses required in SLAs and contracts?
________________________________________



 
Summary of all the questions to be asked to Customer, Business, IT, Security, and Bank stakeholders in one page
Business & Users (WHY & WHO)
•	Who are the users (retail, staff, admin)?
•	What business outcomes define success?
•	Expected growth in users and transactions?
•	Future roadmap (mobile, APIs, external banks)?
•	Risk appetite: security vs usability vs cost?
________________________________________
Functional Scope (WHAT)
•	Customer onboarding & approval flow?
•	Account types, limits, overdrafts, interest rules?
•	Transfers: internal only or external?
•	Bill payments: instant vs scheduled?
•	Cheque processing: manual vs automated?
•	Required reports, statements, reconciliation?
________________________________________
Non-Functional Requirements (HOW WELL)
•	Performance SLAs (login, balance, transfer)?
•	Peak load & concurrency expectations?
•	Availability target (24×7, 99.9%+)?
•	Scalability expectations (today vs 3 years)?
•	Maintenance windows & downtime tolerance?
________________________________________
Application Architecture
•	Monolith vs layered vs service-oriented?
•	Technology stack & standards?
•	Integration with core banking systems?
•	Sync vs async processing?
•	Session & state management approach?
________________________________________
Infrastructure & Deployment
•	On-prem, cloud, or hybrid?
•	Environments (Dev, QA, UAT, Prod)?
•	Load balancing & high availability?
•	Auto-scaling expectations?
•	CI/CD & release strategy?
________________________________________
Data & Storage
•	Database technology & scalability?
•	Data growth & retention policies?
•	Encryption at rest & in transit?
•	Backup, restore, PITR expectations?
•	Data residency & masking needs?
________________________________________
Identity & Access Management (IAM)
•	Authentication method (password, OTP, MFA)?
•	Role-based access for users & staff?
•	Privileged access controls?
•	Account lock/unlock governance?
•	Auditability of access?
________________________________________
Security Controls
•	Secure coding standards (OWASP)?
•	API security approach?
•	Rate limiting & bot protection?
•	Network security (WAF, firewall, segmentation)?
•	Secrets & key management?
________________________________________
Compliance & Governance
•	Regulatory frameworks (RBI, ISO, PCI)?
•	Mandatory audits & approvals?
•	Log retention & tamper-proofing?
•	Pen-testing & security reviews?
•	Documentation & sign-off requirements?
________________________________________
Risk & Fraud
•	Key fraud scenarios to design for?
•	Transaction risk thresholds?
•	Real-time monitoring vs post-facto?
•	Manual vs automated controls?
•	Incident response expectations?
________________________________________
Monitoring & Operations
•	What to monitor (performance, security, business KPIs)?
•	Alerting & escalation paths?
•	SLA & incident resolution times?
•	Operational dashboards required?
________________________________________
Disaster Recovery & Resilience
•	DR required or optional?
•	RTO / RPO targets?
•	Active-active vs active-passive?
•	DR testing frequency?
________________________________________



