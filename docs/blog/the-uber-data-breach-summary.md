---
title: The Uber data breach summary
date: Wed, 28 Sep 2022 16:14:00 +0000
---

Roughly a week ago, *Uber* suffered a data breach in its computer systems which led to internal systems being compromised and inaccessible. The hacker could access Uber source code, emails, and other internal systems. Earlier in the week, Uber provided no specifics, but independent security researchers were able to categorize the attack and dive deep into the specific details.

> **Key Impact**: This breach demonstrated how social engineering combined with MFA fatigue can compromise even large technology companies with robust security measures.

## Attack Overview

The breach initially involved compromising an employee's *Slack account* and broadcasting messages on the company's internal Slack. The attack was attributed to a member of the *Lapsus$* hacking group who goes by the actor name **"teapotuberhacker"**.

### Initial Access Vector

```mermaid
graph TD
A[Attacker] --> B[MFA Fatigue Attack]
B --> C[Employee Receives Multiple MFA Prompts]
C --> D[Employee Gets Frustrated]
D --> E[WhatsApp Message: Fake IT Support]
E --> F[Employee Approves MFA]
F --> G[Attacker Gains Slack Access]
G --> H[Internal Systems Compromised]
```

**Attack Timeline:**

1. **Repeated MFA Notifications**: The hacker repeatedly sent *MFA* notifications to an Uber employee
2. **Social Engineering**: Sent a *WhatsApp message* pretending to be part of Uber's IT team
3. **MFA Approval**: *MFA notification fatigue* led the employee to approve the login
4. **Device Registration**: Attacker registered their device
5. **Slack Access**: Gained access to internal Slack system
6. **Privilege Escalation**: Found admin credentials in PowerShell scripts

> **Attack Vector Note**: This same technique was previously seen in the Mailchimp and Twilio breaches, indicating a repeatable pattern.

## The MFA Fatigue Technique

*MFA fatigue* (also called *MFA bombing* or *MFA spamming*) is when attackers:

1. Obtain valid credentials (username/password)
2. Repeatedly attempt to login, triggering MFA prompts
3. Bombard the user with dozens or hundreds of MFA requests
4. User gets frustrated and approves one to make it stop
5. Attacker gains access

```mermaid
sequenceDiagram
participant Attacker
participant System
participant Employee

loop Every 30 seconds
Attacker->>System: Login Attempt
System->>Employee: Send MFA Prompt
Employee->>System: Deny/Ignore
end

Attacker->>Employee: WhatsApp: "Hi, IT here, approve the MFA"
Employee->>System: Approve MFA (Frustrated)
System->>Attacker: Access Granted
```

## Privilege Escalation

After gaining that initial access and foothold, the hacker found an **internal network share** that contained *PowerShell scripts* with privileged admin credentials, granting access to critical systems:

### Compromised Systems

| **System** | **Access Level** | **Impact** |
|------------|------------------|------------|
| **AWS** | Admin credentials | Cloud infrastructure access |
| **GCP** | Admin credentials | Multi-cloud compromise |
| **OneLogin** | SSO tenant access | Single sign-on compromise |
| **Sentinel One** | Security platform | Disabled security monitoring |
| **Slack** | Full access | Internal communications exposed |
| **HackerOne** | Bug reports | Vulnerability intelligence |

> **Critical Failure**: Storing privileged credentials in easily accessible PowerShell scripts is a severe security misconfiguration.

## PowerShell Abuse

*PowerShell* is a built-in tool/feature within Windows OS. It is used as a legitimate administrative tool but can be weaponized as a **post-exploitation tool**. Abusing PowerShell script execution elevates the security risk for systems to cyber threats such as:

- Code injections
- Malware deployment
- Ransomware distribution
- Credential harvesting
- Lateral movement

**Example of Credential Exposure:**

```powershell
# BAD PRACTICE - Never store credentials like this!
$username = "admin@uber.com"
$password = "SuperSecretPassword123"
$awsAccessKey = "AKIAIOSFODNN7EXAMPLE"
```

## Additional Compromise: Malware Infection

Following the breach, data logs were put on sale, indicating that at least two Uber employees were infected by malware:

### Malware Identified

**1. Raccoon Stealer:**
- Gathers personal information
- Steals passwords
- Exfiltrates browser cookies
- Captures autofill data

**2. Vidar:**
- Collects 2FA authentication data
- Functions as spyware
- Harvests credentials
- Steals cryptocurrency wallets

```mermaid
graph LR
A[Malware Infection] --> B[Raccoon Stealer]
A --> C[Vidar Spyware]

B --> D[Passwords]
B --> E[Cookies]
B --> F[Autofill Data]

C --> G[2FA Codes]
C --> H[Session Tokens]
C --> I[Personal Data]

D --> J[Data Sold on Dark Web]
E --> J
F --> J
G --> J
H --> J
I --> J
```

## HackerOne Exposure

Security researcher *Sam Curry* revealed the hacker gained access to **privately disclosed vulnerability reports** submitted via *HackerOne*, which is part of Uber's Bug Bounty Program.

**Impact:**
- Confidential vulnerability reports exposed
- Researcher identities potentially compromised
- Unpatched vulnerabilities disclosed to attacker
- Trust in bug bounty program damaged

## Attribution: Lapsus$ Group

According to recent reports, the breach was conducted by a member of the *Lapsus$* hacking group. In the past six months, Lapsus$ has targeted high-profile companies:

| **Company** | **Date** | **Data Stolen** |
|-------------|----------|-----------------|
| **Nvidia** | Feb 2022 | Source code, employee data |
| **Samsung** | Mar 2022 | Source code |
| **Okta** | Mar 2022 | Customer data |
| **Microsoft** | Mar 2022 | Source code |
| **Twilio** | Aug 2022 | Customer data |
| **Cloudflare** | Aug 2022 | Limited access |
| **Uber** | Sep 2022 | Internal systems |

> **Threat Actor Profile**: Lapsus$ is known for extortion, data theft, and public disclosure tactics rather than deploying ransomware.

## Key Learnings from the Incident

### 1. Social Engineering Remains Dominant

*Social Engineering* stays one of the most successful and prevalent vectors of attack. Organizations can train users to spot these attack methods, but **human error never disappears**.

**Lesson**: Technical controls must be supplemented with:
- Regular security awareness training
- Realistic phishing simulations
- Clear reporting procedures
- No-blame culture for reporting suspicious activity

### 2. MFA is Necessary but Not Sufficient

*Multi-Factor Authentication* is a robust security layer of protection, but it is insufficient with the ever-evolving threat landscape. It is vital to advance MFA capabilities and stay ahead of adversaries.

**Advanced MFA Strategies:**
- Use **number matching** instead of simple approve/deny
- Implement **context-aware MFA** (location, device, time-based)
- Deploy **FIDO2 hardware keys** for admin accounts
- Set **rate limiting** on MFA attempts
- Alert users to **unusual MFA request patterns**

### 3. Zero Trust Architecture

The need to eliminate implicit trust by verifying and validating every stage of the security process needs to be implemented using *Zero Trust Architecture*. Encryption of data at rest and in transit is crucial.

### 4. Attack Surface Management

It is crucial to determine your organization's **attack surface**:
- External-facing services
- Third-party integrations
- Shadow IT
- Internal network shares
- Cloud storage

### 5. Executive-Level Priority

Cybersecurity should be prioritized at the **executive level**. Acknowledgment should start right from the top of the organization.

## Defense Recommendations

```mermaid
graph TB
A[Uber Breach Defenses] --> B[Technical Controls]
A --> C[Process Controls]
A --> D[People Controls]

B --> E[Advanced MFA]
B --> F[Credential Management]
B --> G[Network Segmentation]

C --> H[Access Reviews]
C --> I[Incident Response]
C --> J[Monitoring & Alerts]

D --> K[Security Training]
D --> L[Awareness Programs]
D --> M[Reporting Culture]
```

### Immediate Actions

| **Area** | **Recommendation** | **Priority** |
|----------|-------------------|--------------|
| **MFA** | Implement number matching, rate limiting | Critical |
| **Credentials** | Remove hardcoded credentials from scripts | Critical |
| **Access** | Regular access reviews, least privilege | High |
| **Monitoring** | Alert on unusual MFA patterns | High |
| **Training** | MFA fatigue awareness training | Medium |
| **Segmentation** | Isolate critical systems | High |
| **Secrets Management** | Use proper vaults (HashiCorp, AWS Secrets Manager) | Critical |

### Long-Term Improvements

1. **Implement Zero Trust Architecture**
 - Never trust, always verify
 - Micro-segmentation
 - Continuous authentication

2. **Advanced Threat Detection**
 - Behavioral analytics
 - Anomaly detection
 - Threat intelligence integration

3. **Credential Security**
 - Secrets management platform
 - Regular rotation
 - Just-in-time access

4. **Security Culture**
 - No-blame reporting
 - Regular training
 - Executive buy-in

## Conclusion

The *Uber data breach* of September 2022 serves as a powerful reminder that even major technology companies with significant security investments can fall victim to well-executed social engineering attacks. The combination of *MFA fatigue*, *poor credential management*, and *inadequate access controls* created a perfect storm that allowed the Lapsus$ group to compromise critical systems.

The breach highlights several critical lessons:
- **MFA is not infallible** - especially against determined attackers using fatigue tactics
- **Credential hygiene matters** - hardcoded credentials in scripts are a disaster waiting to happen
- **Human error is inevitable** - technical controls must account for this reality
- **Defense in depth is essential** - no single control should be a single point of failure

> **Final Takeaway**: The best defense combines technical controls (advanced MFA, secrets management), robust processes (monitoring, incident response), and educated people (awareness training, reporting culture). All three layers are essential.

## References

- [The Hacker News: Uber Blames Lapsus$ for Data Breach](https://thehackernews.com/2022/09/uber-blames-lapsus-hacking-group-for.html)
- [Washington Post: Uber Hack Details](https://www.washingtonpost.com/technology/2022/09/15/uber-hack/)
- [Sam Curry: Uber Breach Analysis](https://samcurry.net/uber-breach/)
- [CISA: MFA Fatigue Attacks](https://www.cisa.gov/news-events/cybersecurity-advisories)
