---
title: Authentication vs Authorization vs Accounting
date: Mon, 19 Apr 2021 12:30:00 +0000
---

**Authentication** and **authorization** are fundamental components of *online security*, working together to safeguard your data. These common security processes are often used in tandem to ensure secure access to systems and resources.

## Understanding Authentication and Authorization

In basic terms:

- **Authentication**: Verifies the *identity* of a user, confirming they are who they claim to be.
- **Authorization**: Determines *what a user can access*, controlling permissions to view or modify resources.

### Real-World Example
When using a shared document, such as a *Google Doc*:
- You *log in* to **authenticate** your identity.
- **Authorization controls** determine whether you can *view* or *edit* the document.

> **Key Insight**: Authentication confirms *who you are*, while authorization defines *what you can do*.

## The AAA Security Framework

Logging into a network or connecting to a *VPN* often involves the **AAA Security Framework**, which stands for:

1. **Authentication**: Identifying the user.
2. **Authorization**: Granting access to specific resources.
3. **Accounting**: Tracking user activity and resource usage.

### How AAA Works
- **Step 1: Authentication**:
    - Users identify themselves, typically with a *username*.
    - Additional *authentication factors* (e.g., passwords or biometrics) prove their identity.
- **Step 2: Authorization**:
    - Once authenticated, users gain access to resources based on their *username* or *role*.
    - Example: An *administrator* has broader access than a *guest* or *user* account.
- **Step 3: Accounting**:
    - Tracks details like *login times*, *resources accessed*, *data transferred*, and *logout times*.

> **Pro Tip**: The AAA framework ensures secure access and provides auditable logs for network activity.

## Authentication Methods

Authentication processes are familiar to most users and include various methods to prove identity:

- **Traditional Methods**:
    - Entering *passwords*.
    - Answering *security questions*.
    - Scanning a *fingerprint* to unlock a smartphone.
- **Password-Less Techniques**:
    - *Multi-Factor Authentication (MFA)*: Uses one-time passcodes sent via *SMS* or other methods.
    - *Single Sign-On (SSO)*: Allows access to multiple systems with one set of credentials.
    - **Benefit**: Generally more secure than passwords alone.

### Local vs. Centralized Authentication
- **Centralized Authentication**:
    - Stores credentials in a *centralized database* for convenience (e.g., SSO).
    - Risk: Potential single point of failure.
- **Local Authentication**:
    - Uses credentials stored on a *local device* (e.g., logging into a server).
    - Benefit: Useful as a backup or for isolated systems.
    - Challenge: Difficult to scale for large networks.

> **Key Consideration**: Choose local authentication for specific use cases, but centralized systems are more practical for broad access management.

### Biometric Authentication
**Biometric authentication** relies on a user’s unique *physical or biological markers*:

- **Examples**: *Fingerprints*, *facial scans*.
- **Process**: Compares user input to stored biometric data in a database.
- **Advantages**:
    - Hard to fake or replicate.
    - Cannot be forgotten or lost like passwords.
- **Applications**: Widely used in *smartphones*, *computers*, and *secure applications*.

### Hardware Authentication
**Hardware authentication** uses a physical device to verify identity:

- **Examples**: *USB security keys*, *security tokens*.
- **Process**: Insert the device into a *USB port* or connect wirelessly to validate access.
- **Benefit**: Provides robust protection, even against *SIM swap attacks* or *lost phones*, when combined with login credentials.

> **Key Risk**: Losing a hardware authenticator can complicate access, so secure storage is critical.

## Authorization: Controlling Access

**Authorization** occurs after successful authentication, verifying whether a user has permission to access requested *content* or *resources*.

### Authorization Mechanisms
- **Access Tokens**:
    - Contain *security credentialing information* about a user’s *privilege level* and *access rights*.
    - Generated after authentication and checked when accessing resources.
- **Role-Based Access Control (RBAC)**:
    - Assigns access privileges based on a user’s *role* (e.g., admin, user, guest).
- **Access Control Lists (ACLs)**:
    - Specify which *users* or *processes* can access specific *objects* or *data* and what *operations* (e.g., read, write) are allowed.

> **Key Insight**: Authorization ensures users only access resources they’re permitted to, maintaining system security.

## Accounting: Tracking and Auditing

Using the **AAA framework**, *accounting* logs detailed information about user activity:

- **Logged Data**:
    - *When* a user logs in or out.
    - *What* resources or data are accessed or transferred.
    - *Who* is using the network and from *where*.
- **Benefits**:
    - Enables *audits* to verify compliance and security.
    - Ensures the *right users* access *appropriate resources* from *correct locations*.
    - Monitors *resource usage* to maintain system integrity.

### Tools for Accounting
A **Security Information and Event Management (SIEM)** system is an efficient tool for collecting and analyzing event data:

- **Functions**:
    - Logs *user activity*, *logins*, and *system events*.
    - Detects *unauthorized access* or *suspicious behavior*.
    - Provides alerts and reports for security monitoring.
- **Impact**: Enhances the ability to prevent and respond to security incidents.

> **Pro Tip**: A SIEM system is critical for maintaining visibility and control over network security.

## Summary of AAA Components

| Component | Purpose | Key Features |
|-----------|---------|--------------|
| **Authentication** | Verifies user identity | Passwords, MFA, biometrics, hardware keys |
| **Authorization** | Controls access to resources | Access tokens, RBAC, ACLs |
| **Accounting** | Tracks user activity | Logs login times, resource usage, audits via SIEM |

## Conclusion

**Authentication** and **authorization**, supported by *accounting* in the AAA framework, are essential for securing *online systems* and *networks*. By implementing robust authentication methods (e.g., *biometrics*, *hardware keys*), precise authorization controls (e.g., *RBAC*, *ACLs*), and comprehensive accounting via tools like *SIEM*, organizations can ensure that only the *right users* access the *right resources* at the *right time*, keeping data and systems secure.