---
title: Email security monitoring best practices
date: Wed, 26 Oct 2022 16:23:00 +0000
---

Phishing is most likely the first step of a sophisticated attack. Phishing costs not only businesses their money but also time, customer retention, and productivity. Phishing is easy to overlook, so it's essential to know methods to secure your information. Investing in email security programs is the best way to safeguard your data.

## Email Indicators of Compromise:

-   Spam Emails
-   Pre-text: Social Engineering technique where an individual lies and provides a false motive to get confidential data.
-   Phishing
    -   Spear phishing: Target a specific person.
    -   Impersonation: The adversary successfully assumes the identity of legitimate parties in a system or comm protocol
    -   BEC (Business Email Compromise): Gains control of an employee's accounts and convince other employees to perform a fraudulent activity.
-   Email Header Analysis
    -   A record of email servers involved in transferring email messages from sender to recipient.
-   Email Content Analysis
    -   The attacker crafts a payload to complete the exploit when the victim opens a link in a message.
    -   MIME (Multipurpose Internet Mail Extensions): The body of an email supports different formats such as HTML, Rich Text Format (RTF), Binary data encoded as base64, ASCII & attachments.
-   Malicious Payloads: Malicious code is implemented with the message body.
    -   Exploit: Target some vulnerabilities in the email client.
    -   Attachment: The message contains a File Attachment that users will execute or open.
    -   Embedded Link: A link composed of a friendly string or shortened URL to hide the identity of the actual target is embedded with the message body.

## Email Server Security

Spoofing attacks can be mitigated by configuring authentication for the email server system.

-   Sender Policy Framework (SPF): DNS record identifying hosts authorized to send mail for the domain, with only one being allowed per domain.
-   DomainKeys Identified Mail (DKIM): Provides cryptographic authentication mechanism for mail utilizing a public key published as a DNS record.
-   (DMARC) Domain-Based Message Authentication, Reporting & Conformance: Framework for ensuring proper application of SPF & DKIM, a policy published as a DNS record.

> **Key Insight**: SPF, DKIM, and DMARC do not solve the problem of Cousin domains

-   Cousin Domain: DNS Domain that looks similar to another name when rendered by a Mail User Agent (MUA)

## Email Message Security

-   Secure/Multi-purpose Internet Mail Extension (S-MIME): The encryption standard adds a digital signature and public key cryptography to traditional MIME extensions. The user is issued a digital certificate with their public key to use S/MIME. Encrypting message with the receiver's public key ensure confidentiality. A digital signature encrypts the hash of the message to maintain integrity & non-repudiation. The client will determine if the digital signature is valid.