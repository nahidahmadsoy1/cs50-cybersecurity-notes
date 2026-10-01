# 🛡️ CS50 Cybersecurity Notes & Study Guide

> Personal study notes on Harvard's **[CS50's Introduction to Cybersecurity](https://cs50.harvard.edu/cybersecurity)**: core concepts, common attacks, and the defenses against them.

**Big idea:** security is not absolute. It is **risk management**, a constant trade-off between security and convenience.

---

## 📋 Table of Contents
1. [Course Overview](#-course-overview)
2. [Fundamentals](#-fundamentals)
3. [Securing Accounts & Identity](#-securing-accounts--identity)
4. [Securing Data & Cryptography](#-securing-data--cryptography)
5. [Securing Systems](#-securing-systems)
6. [Securing Software](#-securing-software)
7. [Preserving Privacy](#-preserving-privacy)
8. [Quick Reference](#-quick-reference)
9. [Resources](#-resources)

---

## 📖 Course Overview

A personal knowledge base documenting my progress through CS50 Cybersecurity. It covers authentication, cryptography, system and network defense, software vulnerabilities, and privacy.

> ℹ️ Section order may differ slightly from the official lecture order. See the [syllabus](https://cs50.harvard.edu/cybersecurity) for the exact structure.

---

## 🧱 Fundamentals

### CIA Triad
| Property | Meaning | Example threat |
|----------|---------|----------------|
| **Confidentiality** | Only authorized parties can access data | Data breach |
| **Integrity** | Data stays accurate and unaltered | Tampering, malicious edits |
| **Availability** | Systems and data are accessible when needed | DDoS, ransomware |

### Threat Modeling
Ask: **who** are you protecting **what** from, and **why**? Defenses should match the realistic threat.

* **Threat actors:** script kiddies, insiders, organized cybercrime, advanced persistent threats (APTs).
* **Weakest link:** usually people (phishing, social engineering), not technology.
* **Defense in depth:** layer multiple controls; never rely on just one.
* **Least privilege:** grant only the access that is strictly needed.

---

## 🔑 Securing Accounts & Identity

### Authentication Factors
1. **Something you know:** passwords, PINs, passphrases
2. **Something you have:** security keys (e.g. YubiKey), authenticator apps (TOTP), SMS codes
3. **Something you are:** fingerprint, face, iris

**Multi-Factor Authentication (MFA)** requires two or more *different* factors, so a stolen password alone is not enough.
> SMS codes are the weakest second factor (SIM swapping). Prefer authenticator apps or hardware keys.

### Passwords
* **Long and unique** beats short and complex. Length matters most.
* **Never reuse passwords.** Reuse enables *credential stuffing*.
* Use a **password manager** to generate and store unique passwords.
* **Passkeys:** passwordless login built on public-key cryptography; resistant to phishing.

### How Sites Should Store Passwords
* **Hashing:** store a one-way hash, never plaintext.
* **Salting:** add a random unique value before hashing so identical passwords produce different hashes and rainbow tables fail.

### Attacks & Mitigations
| Attack | Description | Mitigation |
|--------|-------------|------------|
| Brute force | Try every possible password | Long passwords, rate limiting, lockouts |
| Dictionary | Try common words/passwords | Avoid common passwords |
| Credential stuffing | Reuse leaked credentials on other sites | Unique passwords, MFA |
| Phishing | Fake messages/sites steal credentials | Skepticism, passkeys, hardware keys |

---

## 🔒 Securing Data & Cryptography

### Encryption
* **Symmetric:** one shared secret key encrypts and decrypts (e.g. AES-256). Fast; good for bulk data. Challenge: sharing the key safely.
* **Asymmetric:** a linked key pair. The **public key** encrypts, the **private key** decrypts (e.g. RSA, ECC). Solves key exchange.
* **End-to-end encryption (E2EE):** only sender and recipient can read the message, not even the service provider.

### Integrity & Authenticity
* **Hash functions** (e.g. SHA-256): fixed-size, one-way output used to verify integrity.
* **Digital signatures:** hash + asymmetric crypto, providing authenticity and non-repudiation.
* **TLS/HTTPS:** encrypts data in transit using PKI and certificates.
  > The padlock means the connection is encrypted, **not** that the site is trustworthy.

> **Hashing vs. encryption:** hashing is one-way; encryption is reversible with the key.

### Backups & Deletion
* **3-2-1 backup rule:** 3 copies, on 2 different media, 1 off-site. Best defense against ransomware.
* **Deleting a file doesn't erase it.** Secure deletion means overwriting or physically destroying the media.
* **Full-disk encryption** protects data if a device is lost or stolen.

---

## 🖥️ Securing Systems

* **Updates & patches:** close known vulnerabilities; one of the simplest, most effective defenses.
* **Firewalls:** filter incoming/outgoing traffic by rules; enable network segmentation to isolate sensitive systems.
* **Antivirus / anti-malware:** detects known threats; not a complete solution.
* **Wi-Fi security:** use WPA2/WPA3; treat public Wi-Fi as untrusted.
* **VPNs:** create an encrypted tunnel to protect traffic on untrusted networks. A VPN shifts trust to the provider and doesn't make you anonymous.
* **Physical security:** screen locks, device encryption, controlled physical access.

---

## 💻 Securing Software

### Memory Safety
* **Buffer overflow:** writing beyond a buffer's boundary can corrupt adjacent memory, crash a program, or allow arbitrary code execution.
* **Why C/C++ is prone:** manual memory management and no automatic bounds checking.
* **Mitigations:** bounds checking, memory-safe languages (Rust, Python, Java), OS protections such as ASLR.

### Injection Attacks
Untrusted input is treated as code. Treat **all external input as untrusted**.

* **Validation:** confirm input matches the expected format.
* **Sanitization:** strip or escape harmful characters.
* **SQL Injection (SQLi):** malicious input alters database queries.
  * Prevention: **parameterized queries / prepared statements**.
* **Cross-Site Scripting (XSS):** attacker scripts run in other users' browsers.
  * Prevention: context-aware output encoding and a strict **Content Security Policy (CSP)**.

### Vulnerability Lifecycle
* **Bug → vulnerability → exploit:** a bug becomes a vulnerability when it can be abused.
* **Zero-day:** a vulnerability unknown to the vendor, with no patch yet.
* **CVE:** public identifier for a known vulnerability.
* **Responsible disclosure & bug bounties:** report privately so it can be fixed before going public.

### Malware & Supply Chain
* **Malware types:** viruses, worms, trojans, spyware, ransomware.
* **Supply chain attacks:** compromise software through dependencies or update mechanisms.
* **Dependency management:** regularly scan source code and third-party libraries for known CVEs.
* **Open vs. closed source:** open source allows public review but isn't automatically secure.

---

## 🕵️ Preserving Privacy

* **Tracking:** cookies, tracking pixels (including in emails), and browser fingerprinting follow you across sites.
* **Metadata:** who, when, and where can reveal a lot even when content is encrypted; photos and documents may embed location data.
* **Incognito/private mode:** only stops local history from being saved; sites and ISPs still see your activity.
* **VPN vs. Tor:** a VPN hides traffic from your ISP but trusts the provider; Tor routes through multiple relays for stronger anonymity.
* **De-anonymization:** "anonymous" datasets can often be re-identified by combining them with other data.
* **Data minimization:** share only what's needed and review app permissions regularly.
* **Regulation:** laws like GDPR give people rights over their personal data.

---

## ⚡ Quick Reference

| Term | Meaning |
|------|---------|
| Credential stuffing | Trying leaked username/password pairs on other sites |
| Phishing | Tricking users into revealing credentials via fake messages or sites |
| Salt | Random data added to a password before hashing |
| MFA | Authentication using more than one factor |
| E2EE | Only sender and recipient can read the message |
| Buffer overflow | Writing past a memory buffer's boundary |
| SQLi / XSS | Injection of malicious queries / scripts |
| Zero-day | Vulnerability with no available patch |
| Defense in depth | Layering multiple security controls |
| Least privilege | Granting only the minimum required access |

---

## 🔗 Resources

* [CS50 Cybersecurity course](https://cs50.harvard.edu/cybersecurity)
* [OWASP Top 10](https://owasp.org/www-project-top-ten/)
* [Have I Been Pwned](https://haveibeenpwned.com/)
* [CVE database](https://www.cve.org/)

---

<sub>Notes compiled for personal study. Not an official CS50 resource.</sub>
