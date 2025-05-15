---
title: Hack The Box Edition: Teacher
date: Wed, 28 Jul 2021 13:02:00 +0000
---

The **Teacher** challenge on *Hack The Box* involves compromising a vulnerable *Linux machine* at IP `10.10.10.153` to gain *privileged access* as the *root* user. This post outlines the strategy, tactics, and step-by-step process used to achieve this goal, offering an engaging *capture-the-flag (CTF)* experience.

## Strategy

The primary objective is to *compromise* the target machine and escalate privileges to obtain *root* access.

> **Key Goal**: Gain unauthorized access to the system and retrieve the *root.txt* flag.

## Tactics

The approach combines *network enumeration*, *web exploitation*, *shell access*, and *privilege escalation*:

- Perform a *network scan* to identify open ports and services.
- Use tools like *Nmap*, *Nikto*, and *dirb* to discover vulnerabilities.
- Exploit a *Moodle* service running on an *Apache* server.
- Leverage *credential discovery* via web fuzzing and database access.
- Establish a *reverse shell* to gain initial access.
- Escalate privileges by exfiltrating credentials and exploiting file permissions.

> **Key Insight**: Thorough enumeration and exploitation of misconfigured services are critical for CTF success.

## Exploitation Process

The following steps detail the process to compromise the *Teacher* machine:

1. **Network Enumeration**:
    - Used *Nmap* to scan the target IP `10.10.10.153` for open ports and services.
    - **Findings**:
        - *Port 80*: Hosting an *Apache* server with a *Moodle* service.
    - Ran *Nikto* to scan for vulnerabilities in the web server.
    - Used *dirb* to enumerate accessible directories on the *Moodle* site.

2. **Web Enumeration**:
    - Discovered an *images* directory containing a file named `5.png`.
    - The `5.png` image included a partial password for user *Giovanni*: `Th4C00lTheacha`, noted as missing a character.
    - Used a *web fuzzer* with a *unique character wordlist* to identify the missing character, determining it was `#`.
    - Constructed the full password: `Th4C00lTheacha#`.
    - Logged into the *Moodle* account as *Giovanni* using the password `Th4C00lTheacha#`.
    > **Key Challenge**: Identifying the missing password character required creative fuzzing.

3. **Exploitation**:
    - Identified the *Moodle* version as *3.4* and used *searchsploit* to find relevant exploits.
    - Discovered a *remote code injection* vulnerability in one of the *Moodle* quizzes.
    - Exploited the vulnerability to establish a *reverse shell* via *Ncat*, gaining access to the shell.

4. **Shell Stabilization**:
    - Spawned a *Python TTY shell* to stabilize the initial shell access.
    - Accessed the *MariaDB* MySQL database using credentials found in a *config file*.

5. **Privilege Escalation**:
    - Exfiltrated credentials for user *Giovanni* from the *MySQL* database.
    - Converted the *hashed password* to plaintext, revealing the password `expelled`.
    - Logged into the system via *SSH* as *Giovanni* using the password `expelled`.
    - Gained access to the *user.txt* flag.
    - Navigated to the `/work/tmp/tmp` directory, which contained the *root.txt* flag with *read and write* privileges.
    - Retrieved the *root.txt* flag.

> **Key Insight**: Database credentials and permissive file access enabled rapid privilege escalation.

## Tools Used

The following table summarizes the tools employed during the exploitation:

| Tool           | Purpose                                      |
|----------------|----------------------------------------------|
| *Nmap*         | Network scanning for open ports and services |
| *Nikto*        | Web server vulnerability scanning            |
| *dirb*         | Directory enumeration on the web server      |
| *Web Fuzzer*   | Identifying missing password character       |
| *searchsploit* | Finding exploits for Moodle 3.4              |
| *Ncat*         | Establishing reverse shell connection        |
| *Python*       | Spawning a stabilized TTY shell              |
| *CyberChef*    | Converting hashed password to plaintext      |

## Final Thoughts

The **Teacher** machine on *Hack The Box* is a *captivating* medium-difficulty *CTF challenge*. Having worked with *Moodle* during university, I was particularly curious about this machine. The process of exploiting the *Moodle* service, fuzzing for credentials, and escalating privileges was both *challenging* and *enjoyable*. This challenge underscores the value of *persistence* and *creative exploitation* in penetration testing.

> **Final Rating**: Medium difficulty, highly recommended for CTF enthusiasts!