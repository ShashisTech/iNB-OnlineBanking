# iNB UI/UX Architecture Document

**Version:** 0.1  
**Status:** Initial Draft   
**Owner:** UI/UX Architecture (with Front‑End, Product, Risk, Compliance)  
**Date:** *19 Jan 2026*

***

## 1. Executive Summary

The goal of this UI/UX architecture is to define a **cohesive, accessible, secure, and scalable** experience for iNB’s online banking application covering: Registration & Approval, Home Dashboard, Accounts & Statements, Cheque Deposits, Bill Payments, and Money Transfers. This document aligns UX with product goals, the domain model, security and regulatory constraints, and the delivery model (web-first, mobile‑responsive; ready for mobile app parity).

**Design tenets**

1.  **Trust & Clarity first** (banking-grade feedback, transparency)
2.  **Consistency by system** (design system & tokens, reusable patterns)
3.  **Performance is UX** (fast, stable interactions; clear skeleton states)
4.  **Accessibility by default** (WCAG 2.1 AA)
5.  **Secure by design** (MFA, lockout handling, secure session UX)
6.  **Observability of behavior** (instrumented flows; measurable)

***

## 2. Scope & Assumptions

**In scope (MVP):**

*   Customer Registration with approval workflow (view-only until activation)
*   Post-login Home Dashboard (balances, quick actions, alerts)
*   Accounts: mini (last 5) + detailed statements (date range)
*   Cheque Deposits: online slip(s), print, status tracking with lifecycle
*   Bill Payments: immediate & scheduled; status and receipts
*   Money Transfers: intra-bank transfers; beneficiary basics
*   Security UX: login, MFA, lockout, session management
*   Accessibility, responsive web, English (i18n-ready)

**Out of scope (MVP, future-ready):**

*   External rails (NEFT/RTGS/IMPS/UPI), corporate maker‑checker, multi-language, advanced personalization, card features.

**Assumptions:**

*   Single interest rate for Savings; daily overdraft interest for Current per case study.
*   Status updates for cheques can originate from operations systems (manual or feed).
*   CBS is the system of record; app is a consumer + cache for read performance.

***

## 3. Target Users & Roles

*   **Retail Customer**: Self-service banking; mobile-first behavior.
*   **Banker/Operations**: Cheque reconciliation, status management.
*   **Admin/Support**: Account unlock, profile support, audit lookup.
*   **Auditor/Compliance (read-only)**: Reports, immutable logs.

Each role maps to a **role-based navigation** and permissioned UI actions.

***

## 4. Experience Architecture (End-to-End)

### 4.1 Global Navigation Model

*   **Top Bar:** Brand, global search (future), profile menu, notifications.
*   **Left Navigation (persistent):** Home, Accounts, Cheques, Payments, Transfers, Support.
*   **Utility Footer:** Legal, privacy, help center, accessibility.

**Navigation principles**

*   Depth ≤ 2 where possible; clear breadcrumbs on detailed screens.
*   Back/forward browser-safe; no dead ends; contextual help panels.

### 4.2 Page Types & Layout Grid

*   **Page Types:** Dashboard, List, Details, Wizard (multi‑step), Receipt/Confirmation, Settings.
*   **Grid:** 12‑column responsive grid; breakpoints: ≥1280 (desktop), 768–1279 (tablet), ≤767 (mobile).
*   **Density:** Comfortable (default), Compact (opt-in) for power users.

### 4.3 Key Journeys & Interaction Patterns

**A) Registration & Approval**

*   Multi‑step wizard: 1) Personal details 2) Contact & Address 3) KYC 4) Account selection 5) Review & Submit.
*   Progressive disclosure for advanced fields; immediate field validation; inline error hints.
*   Post‑submission: “Request received” with reference number, SLA, and status tracking link (before login).
*   Activation: first‑time login with OTP + forced password setup + device recognition.

**B) Home Dashboard**

*   Top: Total relationship snapshot (all accounts).
*   Cards: **Accounts** (balance & last 2 txns), **Quick Actions** (Pay Bill, Transfer, Deposit Cheque), **Upcoming** (scheduled payments), **Alerts** (lockout, low balance, cheque bounced).
*   Personalization: reorder/hide cards (stored per profile).

**C) Accounts & Statements**

*   Accounts list with type, balance, overdraft indicator.
*   Account details: tabs → **Overview**, **Transactions**, **Statements**.
*   Mini statement (last 5) surfaced inline; **Detailed** filter (date from/to, amount range, type).
*   Export: CSV/PDF; pagination & infinite scroll options (performance-dependent).
*   Empty and no‑result states designed with clear next steps.

**D) Cheque Deposits**

*   Deposit slip builder: add multiple cheques per batch, validate MICR/date, print slip with QR/barcode.
*   Status tracker: timeline view (Not Received → Sent for Clearance → Cleared/Bounced).
*   Bounce scenario: fee banner, help CTA, resubmit action.

**E) Bill Payments**

*   Biller selection with smart search; validation per biller (account number/consumer ID).
*   Immediate vs. Scheduled (date picker honors holidays/cut‑offs; show earliest execution).
*   Confirmation with fee/limit info; receipt with reference; retry on async failure with clear messaging.

**F) Money Transfers (Intra‑bank)**

*   Beneficiary add (name, account ID) with cool‑off (configurable); first‑time low limit.
*   Transfer form shows available balance, limits, and estimated posting time; OTP step-up for high values.
*   Success receipt + “Save beneficiary” prompt (if ad‑hoc).

**G) Security & Session UX**

*   Lockout after 3 invalid attempts: friendly, non‑revealing error; **Self‑service unlock** via OTP or route to support.
*   Idle timeout warning with countdown; “Stay signed in?” prompt; safe session end with clear messaging.

***

## 5. Design System & Tokens

**Foundations**

*   **Color:** Primary (bank blue), Success (green), Warning (amber), Critical (red); contrast ≥ 4.5:1.
*   **Typography:** Sans stack; line-height 1.5; accessible sizes (base 16px; scale 1.125).
*   **Spacing:** 4px unit scale.
*   **Elevation:** 0/1/2 for surfaces; focus ring visible at 2px.

**Components (selected)**

*   AppShell (Header, LeftNav, Content), PageHeader, Card, Table (virtualized), Tabs, Stepper, Form (Field, Label, Help, Error), DatePicker, Modal/Drawer, Toast, Skeleton, Empty State, Tag/Badge, Pagination, Breadcrumb, CTA Buttons.

**States & Feedback**

*   Loading (skeletons), Saving (button progress), Success/Warning/Error banners.
*   Disabled vs. read-only states; optimistic UI only where idempotency is guaranteed.

**Internationalization**

*   All strings externalized; number/currency/date localized; bidi-safe (future RTL).

***

## 6. Accessibility (WCAG 2.1 AA)

*   **Keyboard**: Full navigation & operation; visible focus order matches DOM order.
*   **Screen Readers**: Landmarks (header/nav/main/footer), semantic HTML, ARIA for dynamic components.
*   **Contrast & Motion**: Sufficient contrast; reduced motion preference honored.
*   **Forms**: Labels, descriptions, error associations, inline guidance; validation summarized.
*   **Media/Icons**: Accessible names; non‑decorative icons have `aria-label` or text.

***

## 7. Content Design & Messaging

*   **Tone**: Clear, respectful, non‑alarmist; avoids jargon.

*   **Microcopy patterns**:
    *   Errors: “We couldn’t complete that transfer. Your account was **not debited**. Try again or contact support.”
    *   Confirmations: “Payment scheduled for **Tue, 23 Jan, 10:00 AM**.”
    *   Security: “You have 1 attempt left before your account locks.”

*   **Templates**: Receipt, Notification (email/SMS), Empty states, Help tooltip library.

***

## 8. Data & Domain Alignment (UX ↔ ER Model)

Mapping primary entities to UI areas for **consistency and traceability**:

| Domain Entity | Primary UI Surfaces                          |
| ------------- | -------------------------------------------- |
| Customer      | Registration wizard, Profile & Settings      |
| Account       | Dashboard card, Accounts list & details      |
| Transaction   | Account → Transactions, Exports              |
| Cheque        | Cheque slip builder, Cheque status timeline  |
| BillPayment   | Billers list, Pay wizard, Scheduled payments |
| MoneyTransfer | Beneficiaries, Transfer form, Receipts       |

**Identifiers** (masked or short refs) surface in receipts and status trackers to support support/audit without exposing sensitive data.

***

## 9. Security UX

*   **AuthN**: Username (case-insensitive), strong password policy (prefer passphrases), OTP for high‑risk actions.
*   **AuthZ**: UI gates by role/entitlement; sensitive controls hidden.
*   **Privacy**: Mask PII/PCI‑like fields; copy disabled where required; explicit consent flows where applicable.
*   **Session**: Short idle timeout with “extend” prompt; clear logout; device/session list for users to revoke access.
*   **Errors**: Avoid disclosing auth reason (“Invalid credentials” generic); audit-friendly correlation IDs on error screens.

***

## 10. Performance & Resilience (UX View)

*   **Budgets**: P95 page TTI ≤ 2.5s desktop, ≤ 3.5s mobile on 4G; key action latency ≤ 1.5s.

*   **Tech patterns**:
    *   Server‑driven pagination & query filters for statements.
    *   Virtualized tables, incremental rendering, skeletons.
    *   Caching: balances & statement summaries with safe TTL; cache-busting on updates.
    *   Idempotent actions (payments/transfers) with retry-safe UI.

*   **Offline/Intermittent** (future mobile): graceful retries, “queued” states, clear sync feedback.

***

## 11. Telemetry & Experimentation

**Instrumentation plan**

*   **Events:** Registration step view/complete, Dashboard card interactions, Filters applied, Payment/Transfer initiate/confirm/fail, Cheque slip created/printed/status view.
*   **KPIs:** Task completion rate, time on task, drop‑off by step, error rate by field, P95 latency per flow, accessibility violations count.
*   **A/B tests (post-MVP):** Dashboard card layouts; bill pay confirmation density; default filters on statements.

All events include **anonymized** user and session IDs; PII excluded from analytics.

***

## 12. UI Inventory & Deliverables

*   **High‑fidelity reference screens** (desktop + mobile breakpoints) for all key journeys
*   **Flow diagrams**: Registration, Bill Pay (immediate/scheduled), Money Transfer, Cheque lifecycle
*   **Design system**: Tokens JSON, component specs (usage, props, states), accessibility notes
*   **Content kit**: Microcopy, receipts, notifications templates
*   **Prototype**: Click‑through (Figma/Framer) for usability validation

***

## 13. Handover to Engineering

*   **Spec format**:
    *   Screen specs with redlines (spacing, sizes, states)
    *   Interactive component specs (focus, keyboard, ARIA)
    *   Token file (JSON) → FE build pipeline (e.g., CSS variables)
    *   Acceptance criteria per story (UX + accessibility + performance)

*   **Front‑end architecture alignment** (example):
    *   **Pattern**: Micro‑frontends (optional) or single SPA with **BFF**
    *   **Framework**: React + TypeScript, component library built from tokens
    *   **Routing**: URL structure mirrors IA; route guards based on auth/entitlements
    *   **State**: Query library for server cache; local store for UI state only
    *   **Error handling**: Central boundary; standardized error UI

***

## 14. Governance & Lifecycle

*   **UX checkpoints**: Inception (vision), Pre‑build (design review), Pre‑UAT (accessibility/perf review), Pre‑launch (content/consent/comms), Post‑launch (telemetry readout).
*   **Design system governance**: RFC process for new components; versioning & deprecation rules.
*   **Accessibility audits**: Automated + manual every release; defect SLAs by severity.
*   **Change management**: Feature flags and dark launches for impactful UX changes.

***

## 15. Risks & Mitigations

| Risk                                  | Impact          | Mitigation                                                   |
| ------------------------------------- | --------------- | ------------------------------------------------------------ |
| Fragmented patterns across teams      | Inconsistent UX | Central design system + governance reviews                   |
| Performance regressions on statements | Abandonment     | Server-side pagination + virtualized UI + budgets            |
| Accessibility failures                | Compliance risk | WCAG checklists, automated scans, expert audits              |
| Ambiguous cheque lifecycle            | User confusion  | Timeline UI + explicit SLAs + notifications                  |
| Payment/transfer failure UX           | Support load    | Clear receipts, resilient retries, non-duplication messaging |

***

## 16. Open Questions (to finalize with stakeholders)

1.  Registration KYC providers & exact data capture?
2.  Lockout: self‑service unlock via OTP allowed for MVP?
3.  Bill pay rails (BBPS?) and cut‑off/holiday handling specifics?
4.  Transfer limits, beneficiary cool‑off, and OTP thresholds?
5.  Cheque slip print requirements (barcode/QR format)?
6.  Statement export formats + legal archiving rules (PDF signing)?
7.  Languages for phase‑2; right‑to‑left support?
8.  Target SLOs (availability, latency) for UX performance budgets?

***

## 17. Appendix

### A. Screen Inventory (MVP)

*   **Public**: Landing, Registration Wizard (5 steps), Registration Status
*   **Auth**: Login, MFA, Account Lockout/Unlock
*   **App**: Dashboard, Accounts (List/Details/Transactions/Statements), Cheques (Create Slip/Status), Bill Pay (Select/Add Biller, Pay Now/Schedule, Receipts), Transfers (Beneficiaries, Transfer, Receipts), Notifications, Profile/Settings, Support

### B. Example Acceptance Criteria (sample)

*   **Statement filter**: Keyboard navigable; applies within 300ms; P95 API ≤ 800ms; results visible count announced to screen reader.
*   **Bill pay confirmation**: Displays execution date/time respecting cut‑offs; receipt downloadable within 2s; error states non-destructive.

***


