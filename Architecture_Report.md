**Architecture Explanation**

**Indian Net Bank (iNB) – Online Banking System**

**1\. Overview**

The iNB Online Banking System is designed using a **multi-tier layered architecture** to ensure scalability, security, maintainability, and high performance. The system supports core banking functionalities such as customer registration, account management, money transfers, cheque processing, bill payments, reporting, and secure authentication.

The architecture is divided into the following main layers:

1.  Presentation Layer
2.  Application / Service Layer
3.  Data Layer
4.  Security and External Services
5.  Backup and Monitoring

Each layer has a clearly defined responsibility, ensuring separation of concerns and easier system management.

**2\. Presentation Layer**

The Presentation Layer represents the **user interface** of the system. It is implemented using an **ASP.NET Web Application** that can be accessed through web browsers and mobile devices.

**Responsibilities:**

*   User login and authentication screens
*   Customer registration forms
*   Dashboard showing account details
*   Viewing mini and detailed statements
*   Money transfer and bill payment forms
*   Cheque deposit and status tracking

**Features:**

*   Communicates with the Application Layer through **secure HTTPS API calls**
*   Ensures consistent look-and-feel across all pages
*   Provides easy navigation for customers and bank staff

This layer does not contain business logic. It only handles user interaction and data display.

**3\. Application / Service Layer**

The Application Layer contains the **core business logic** of the system. It processes all requests coming from the Presentation Layer and enforces banking rules and validations.

**Main Services:**

*   **Auth Service**  
    Handles user authentication, password validation, login attempts, and account locking after three failed attempts.
*   **Account Service**  
    Manages savings and current accounts, balance updates, interest calculation, and overdraft processing.
*   **Cheque Service**  
    Handles cheque deposit requests, status updates (Not Received, Sent for Clearance, Cleared, Bounced), and fine deduction for bounced cheques.
*   **Payment Service**  
    Manages bill payments, scheduled payments, and money transfers between iNB accounts.
*   **Report Service**  
    Generates reconciliation reports and transaction statements for customers and bank staff.
*   **Notification Service**  
    Sends email or SMS notifications for account approval, transactions, and important alerts.

**Responsibilities:**

*   Enforces business rules
*   Validates user inputs
*   Applies security checks
*   Communicates with the database using SQL queries
*   Integrates with external services

This layer ensures that all banking operations follow defined policies and regulations.

**4\. Data Layer**

The Data Layer uses a **SQL Server Database** to store all system data securely.

**Stored Data Includes:**

*   Customer information
*   Account details (Savings / Current)
*   Transaction records
*   Cheque deposit records
*   Bill payment details
*   Login attempts and audit logs

**Responsibilities:**

*   Ensures data integrity and consistency
*   Supports transaction management
*   Provides fast data retrieval
*   Maintains audit trails for security and compliance

All data access is controlled by the Application Layer to prevent unauthorized access.

**5\. Security**

Security is a critical part of the iNB Online Banking System.

**Security Measures:**

*   **HTTPS communication** between users and the system
*   **Password encryption** and secure authentication
*   **Account lock** after three consecutive failed login attempts
*   **Role-based access** for customers and bank staff
*   **Audit logs** for tracking login and transaction activities

These measures ensure data confidentiality, integrity, and system reliability.

**6\. External Services**

The system integrates with external services for enhanced functionality:

*   **Email / SMS Gateway** – for notifications and alerts
*   **Payment APIs** – for bill payments and financial transactions

These services are accessed through secure APIs from the Application Layer.

**7\. Backup and Monitoring**

To ensure high availability and reliability, the system includes:

*   Regular **database backups**
*   **System monitoring** for performance and errors
*   **Log management** for troubleshooting
*   **Alert mechanisms** for failures

This helps in disaster recovery and ensures uninterrupted banking services.

**8\. Conclusion**

The layered architecture of the iNB Online Banking System provides a robust, secure, and scalable foundation for online banking operations. By separating the system into Presentation, Application, and Data layers, the architecture ensures maintainability, improved security, and better performance. The integration of security mechanisms, external services, and backup systems makes the solution suitable for real-world banking environments.