# UI/UX Architecture – Key Concepts & Terms

Below is a breakdown of the most important terms used in the document, *grouped by topic*, with short, presentation‑friendly explanations.

***

# 1. **Experience Architecture**

Experience Architecture refers to the **overall structure** of how users navigate, interact, and complete tasks across the product.

### **Key Concepts**

### **Navigation Model**

Defines how users move across the product: the menu system, top bar, side bar, breadcrumbs.  
Think of it like the *site map* + *workflow map*.

### **Page Types**

Standard layouts such as:

*   Dashboard
*   List pages
*   Detail pages
*   Wizards (multi-step flows)
*   Receipts

Using consistent page types improves usability because users always know what to expect.

### **Layouts / Grid System**

A layout grid ensures consistent spacing and alignment across pages.  
Example: **12‑column grid** — the industry standard used in responsive web design.

***

# 2. **Design System**

A **design system** is a reusable library of building blocks (buttons, forms, typography, colors) used across all screens.  
It ensures everything looks and behaves consistently.

### **Tokens**

The smallest design values:

*   Color tokens
*   Font tokens
*   Spacing tokens
*   Shadow/elevation tokens

Developers use these to style components consistently.

### **Components**

Reusable UI elements:

*   Button
*   Card
*   Table
*   Tabs
*   Form controls
*   Modals

Architects define how each behaves, interacts, and scales.

***

# 3. **Information Architecture (IA)**

IA defines **how information is organized and structured** in the app.

### **Examples**

*   Categorizing features into sections: Accounts, Payments, Transfers
*   Creating clear labels
*   Grouping related info under tabs
*   Defining the hierarchy of pages

Good IA reduces cognitive load and helps users find things quickly.

***

# 4. **User Journey / User Flow**

A **user journey** maps the step‑by‑step actions users take to achieve a goal.

Examples:

*   Registering an account
*   Paying a bill
*   Depositing a cheque
*   Viewing account statements

Journeys are used to plan screens, dialogs, validation, and system interactions.

***

# 5. **Interaction Patterns**

Standard ways users interact with the interface.

### Examples

*   **Inline validation** – Errors appear immediately when a field is wrong.
*   **Progressive disclosure** – Show advanced options only if needed.
*   **Wizard flow** – Easy step-by-step progression.
*   **Skeleton screens** – Blank loading shapes instead of spinners.

Patterns make the interface predictable and reduce friction.

***

# 6. **Accessibility (WCAG 2.1 AA)**

Accessibility ensures the app can be used by people with disabilities.

### **Standards Referenced**

**WCAG 2.1 AA** — international standard applied in banking and government websites.  
Examples:

*   Sufficient color contrast
*   Keyboard navigation
*   Screen-reader compatible layouts
*   Focus indicators
*   ARIA attributes

These are essential for compliance and inclusive design.

***

# 7. **Microcopy / Content Design**

Microcopy means **short, helpful text** that supports the user.

Examples:

*   Error messages
*   Button labels
*   Tooltips
*   Success messages
*   Confirmation texts

Good microcopy reduces user mistakes and confusion.

***

# 8. **Security UX Concepts**

### **MFA (Multi-Factor Authentication)**

Requires 2 types of verification (password + OTP).

### **Account Lockout UX**

After too many failed attempts, the account locks.  
UX ensures:

*   Non‑revealing messages
*   Clear next steps
*   Self‑service unlock (if allowed)

### **Session Timeout UX**

When users are inactive, the session expires.  
UX requires:

*   Warning dialog
*   Auto‑logout
*   Security messaging

***

# 9. **Performance Concepts**

### **TTI (Time to Interactive)**

How fast a page becomes usable.  
A key UX metric.

### **Skeleton Screens**

Gray placeholders shown while data loads — feels much faster than a spinner.

### **Server-Side Pagination**

Only load data in small chunks (e.g., 20 rows at a time) — critical for banking statements.

### **Virtualized Tables**

Only render rows currently visible on the screen — boosts performance.

***

# 10. **Telemetry / Analytics Terms**

These measure how real users behave in the app.

### **Events**

Recorded interactions such as:

*   Click on “Pay Bill”
*   Filter applied
*   Transfer completed

### **KPIs**

Key UX performance indicators:

*   Drop-off rate
*   Error rate
*   Time on task
*   Success rate

### **A/B Testing**

Testing two versions of a design to see which performs better.

***

# 11. **Governance & Lifecycle Terms**

### **Design Review**

Architect ensures designs follow standards.

### **UX Checkpoints**

Approval gates inside the SDLC (software development lifecycle).

### **Feature Flags**

Enable or disable new features without redeploying code — used for gradual UX rollout.

### **Accessibility Audits**

Automated + manual checks to ensure compliance.

***

# 12. **Domain Concepts (related to the case study)**

### **Mini Statement**

Last 5 transactions; quick view.

### **Detailed Statement**

A date-range filter with export options (CSV/PDF).

### **Cheque Lifecycle**

Not Received → Sent for Clearance → Cleared/Bounced.

### **Bill Payment Scheduling**

Payments scheduled for future dates; needs cut-off rules.

### **Intra-bank Transfer**

Transfer between accounts within the same bank — faster settlement.

These domain concepts inform UX flows and data structure.

***

