Indian Net Bank (iNB) – Governance & Compliance Policy

Version: 1.0

Policy Owner: Arunava Patra (Governance & Compliance)

Approvers: Shashi Shekhar

Classification: Internal

Effective Date: TBD

Review Cycle: Annual or upon significant change

# 1. Purpose

This policy establishes the governance and compliance framework for the Indian Net Bank (iNB) Online Banking System. It ensures security, regulatory compliance, auditability, data protection, and controlled operations across all system components.

# 2. Scope

This policy applies to the Presentation Layer, Application / Service Layer, Data Layer, Analytics & Reporting components, external integrations, infrastructure, and all users of the iNB Online Banking System.

# 3. Governance Objectives

The objectives of governance are to protect customer data and financial assets, ensure regulatory compliance, enable audit readiness, enforce accountability, and maintain system stability and performance.

# 4. Governance Principles

Security by design, least privilege, separation of duties, centralized configuration control, and controlled change management.

# 5. Roles & Responsibilities

Governance & Compliance: Arunava Owns this policy, defines governance controls, manages risk, and provides final compliance sign-off.

Security: Team Responsible for authentication, authorization, encryption, and infrastructure security.

Architecture: Team Ensures architectural alignment with governance, security, and scalability requirements.

Database & Data Management: Team Owns data integrity, backups, recovery, and retention.

UI/UX Lead: Team Ensures secure, consistent, and user-friendly responsive interfaces.

Requirements: Team Captures functional, regulatory, and compliance requirements.

Analytics & Reporting: Team Responsible for analytics governance, report accuracy, compliance dashboards, and audit reporting.

# 6. Access Control & Authentication

Role-based access control (RBAC) is mandatory. User accounts are locked after three consecutive invalid login attempts. All access and authentication events must be logged.

# 7. Data Protection & Privacy

Sensitive customer and financial data must be protected in transit and at rest. Personally Identifiable Information (PII) must be minimized, masked where required, and excluded from logs and analytics outputs.

# 8. Transaction & Account Governance

All transactions must be validated, authorized, logged with before-and-after balances, and processed in accordance with defined banking rules.

# 9. Cheque Processing Governance

Cheque deposits follow a controlled lifecycle: Not Received, Sent for Clearance, Cleared, or Bounced. Every status transition is auditable and subject to reconciliation.

# 10. Analytics & Reporting Governance

Analytics and reports are read-only, time-stamped, reproducible, and version-controlled. Compliance and audit reports must be retained as per policy.

# 11. Audit Logging & Monitoring

Audit logs must capture authentication attempts, financial transactions, administrative actions, configuration changes, and report access. Logs must be tamper-resistant and centrally monitored.

# 12. Change Management

All production changes require approval. Configuration changes are logged and subject to review. Emergency changes require post-implementation review.

# 13. Incident Management

Security and operational incidents must be identified, classified, investigated, resolved, and documented. Root Cause Analysis is mandatory for major incidents.

# 14. Backup, Disaster Recovery & Continuity

Regular backups, restoring testing, and defined recovery objectives ensure continuity of banking services.

# 15. Compliance, Review & Approvals

Compliance with this policy is mandatory. The policy is reviewed annually or upon major changes.

Policy Owner: Arunava Patra

Approver: Shashi Shekhar