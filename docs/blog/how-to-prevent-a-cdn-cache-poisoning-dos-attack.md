---
title: How to prevent a Cache Poisoning DoS Attack?
date: Wed, 08 Jun 2022 16:15:00 +0000
---

**Cache poisoning** occurs when an *attacker* manipulates an *HTTP request* to trick a *web server* into serving a *malicious resource* with the same *cache key* as a legitimate request, contaminating the *cache* and affecting *users*. A **Denial of Service (DoS)** attack aims to disrupt *network resources* by flooding a *host* with *unintended traffic*, causing *crashes*. A **Cache Poisoning DoS (CPDoS)** attack combines these, targeting *intermediate cache proxy servers* to deliver *error responses*, halting access to *web resources*. This guide outlines *cache poisoning*, *DoS attacks*, *CPDoS attack mechanisms*, their *types*, and *protection strategies*.

## Understanding Cache Poisoning

*Cache poisoning* involves an *attacker* sending an *HTTP request* that deceives a *web server* into caching a *malicious resource*:

- The *malicious resource* shares the same *cache key* as a legitimate request.
- Once cached, it is served to *users* attempting to access the *resource*, compromising *security* or *functionality*.

> **Key Concept**: *Cache poisoning* exploits *caching mechanisms* to deliver *malicious content* to *unsuspecting users*.

## Denial of Service (DoS) Attacks

A *DoS attack* seeks to make a *machine* or *network resource* unavailable to *users* by disrupting *services*:

- *Attackers* flood the *target* with *unintended traffic*.
- This overwhelms the *host*, resulting in *crashes* or *service unavailability*.

> **Key Threat**: *DoS attacks* disrupt *critical services*, impacting *user access* and *business operations*.

## Cache Poisoning DoS (CPDoS) Attacks

A *CPDoS attack* targets an *intermediate cache proxy server* between the *client* (victim) and *web server* with *malicious HTTP requests*:

- The *attacker* configures the *cache response* with *error-related codes* (e.g., `400 Bad Request`), blocking access to *web resources*.
- *CPDoS* poses a *high risk* due to its *stealth* (minimal detection risk) and *impact* on *mission-critical websites* (e.g., *educational*, *government*, *banking*, *medical*).

> **Key Risk**: *CPDoS attacks* silently disrupt *critical web resources* with *high success rates*.

## Working of a CPDoS Attack

The *CPDoS attack workflow* involves the following steps:

1. An *attacker* sends an *HTTP request* with a *malicious header* targeting the *victim’s resources*.
2. The *intermediate cache server* processes the *request*, forwarding the *malicious header* discreetly to the *origin server*.
3. The *origin server* identifies the *malicious request* and responds with an *error message*.
4. The *cache server* stores the *error response* instead of the *requested resources*.
5. The *attacker* receives the *error response*, confirming the *attack’s success*.
6. Subsequent *legitimate user requests* receive the *cached error message*, denying access.

> **Key Workflow**: *CPDoS* leverages *cached error responses* to *block legitimate access*.

## Types of CPDoS Attacks

The table below summarizes the *types* of *CPDoS attacks* and their *mechanisms*:

| **Attack Type**            | **Mechanism**                                                                                                                                                                                                                 |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| HTTP Header Oversize (HHO) | Exploits *cache servers* accepting *larger header sizes* than the *origin server*. The *attacker* sends a *GET request* exceeding the *origin server’s limit* but within the *cache’s limit*, triggering an *error response*. |
| HTTP Meta Character (HMC)  | Inserts *malicious meta characters* (e.g., `\n` (linebreak), `\r` (linefeed), `\a` (bell)) in the *HTTP request* to *bypass the cache*. The *origin server* flags these as *malicious*, returning an *error message*.         |
| HTTP Method Override (HMO) | Uses headers like `X-HTTP-Method-Override` to *tunnel blocked HTTP methods* (e.g., *DELETE* via *POST*). The *override* causes the *origin server* to misinterpret the *request*, generating an *error response*.             |

> **Key Types**: *HHO*, *HMC*, and *HMO* exploit *cache discrepancies* to *induce errors*.

## Protecting Against CPDoS Attacks

Effective *protection strategies* mitigate *CPDoS attacks* and ensure *web resource availability*:

- **Error Code Management**:
    - Cache *error messages* based on *HTTP standard policies* (e.g., `404 Not Found`, `405 Method Not Allowed`, `410 Gone`, `501 Not Implemented`).
    - Use `431 Request Header Fields Too Large` for *oversized headers* instead of `400 Bad Request` or `404 Not Found`.
- **CDN Configuration**:
    - Properly configure *Content Delivery Networks (CDNs)* to handle *error codes* accurately, avoiding *generic responses* like `400 Bad Request`.
- **Cache Control**:
    - Exclude *error pages* from *caching* by adding the header `Cache-Control: no-store` to each *error page*.
    - Mitigates *HHO* and *HMC* by preventing *error response caching*.
- **Web Application Firewall (WAF)**:
    - Deploy a *WAF* to *block malicious requests* before they reach the *origin server*.
    - Choose a *WAF* with *secure CDN*, *DoS protection*, *SSL integration*, *intelligent caching*, and *robust customer support*.

> **Key Protection**: *Proactive configuration* and *WAF deployment* safeguard against *CPDoS attacks*.

## Conclusion

**Cache Poisoning** and **CPDoS attacks** exploit *caching mechanisms* to disrupt *web resources*, posing *significant risks* to *mission-critical websites*. By understanding *cache poisoning*, *DoS attacks*, and the *CPDoS workflow*, organizations can identify vulnerabilities. The *HHO*, *HMC*, and *HMO* attack types leverage *header discrepancies* and *method overrides* to *cache error responses*, blocking *legitimate access*. Implementing *proper error code management*, *CDN configurations*, *cache controls*, and *WAFs* mitigates these *threats*. Regular *monitoring* and *configuration reviews* ensure *resilient defenses*, maintaining *service availability* and *user trust*.

> **Final Takeaway**: A *strategic defense* against *CPDoS attacks* protects *critical web resources* and ensures *operational continuity*.
