# 🔐 CS50 Cybersecurity — Week 1: Securing Accounts

## 📌 Executive Summary
A comprehensive deep-dive into account security architecture, identity management, cryptographic password dynamics, multi-factor authentication (MFA) mechanisms, and threat mitigation models.

---

## 🎯 Threat Modeling & Attack Vectors

### 1. Credential & Password Exploits
* 🪓 **Brute-Force Attack:** Exhaustive computation testing all possible character permutations until valid credentials are discovered.
* 📖 **Dictionary Attack:** Targeted guessing using pre-compiled wordlists, cracked hash databases, and common password variations.
* 🔄 **Credential Stuffing:** Automated replay of leaked username/password pairs from third-party breaches across unrelated services.
* 🚿 **Password Spraying:** Testing a single common password (e.g., `Spring2026!`) against thousands of distinct accounts to evade IP-based lockout thresholds.

### 2. Social Engineering & Interception
* 🎣 **Phishing & Spear Phishing:** Deceptive communication designed to trick targets into submitting credentials on fake authentication portals.
* 📱 **SIM-Swapping:** Convincing mobile network operators to transfer a victim's phone number to an attacker's SIM, hijacking SMS-based 2FA.
* 🍪 **Session Hijacking & Cookie Theft:** Exfiltrating session tokens via Cross-Site Scripting (XSS) or malware to bypass authentication entirely.

---

## 🧠 Core Security Mechanics & Concepts

### 1. Identity & Access Control
* 🆔 **Authentication (AuthN):** Verification of claimed identity (*"Who are you?"*).
* 🛂 **Authorization (AuthZ):** Granting access rights and permission boundaries (*"What are you allowed to do?"*).

### 2. Mathematical Password Entropy
Password entropy measures the unpredictability of a passphrase in bits:

$$E = L \times \log_2(R)$$

* **$E$** = Entropy in bits
* **$L$** = Password length (number of characters)
* **$R$** = Size of the character pool (e.g., 26 lowercase + 26 uppercase + 10 digits + 32 symbols = 94)

💡 **Key Takeaway:** Exponential scaling through length ($L$) provides significantly greater resistance against brute-force attacks than character complexity ($R$).

### 3. Multi-Factor Authentication (MFA) Architecture
Authenticators must combine at least two factors from distinct security boundaries:
* 🧠 **Something You Know (Knowledge):** Passwords, PINs, security answers.
* 📲 **Something You Have (Possession):** Time-based One-Time Passwords (TOTP via RFC 6238), hardware keys (FIDO2/WebAuthn YubiKeys), SMS codes.
* 👁️ **Something You Are (Inherence):** Biometric traits (fingerprints, facial geometry, retina scans).

---

## 🛡️ Defense-in-Depth & Mitigation Strategies

* 🔑 **Zero-Knowledge Password Managers:** Store credentials using AES-256 encryption client-side (e.g., Bitwarden).
* 🗝️ **Phishing-Resistant MFA:** Transition away from SMS/TOTP toward FIDO2/WebAuthn standard hardware tokens to prevent adversary-in-the-middle (AiTM) proxy attacks.
* 🎟️ **Session & Token Management:** Enforce short-lived session cookies with `HttpOnly`, `Secure`, and `SameSite=Strict` flags.
* 📝 **Least Privilege & OAuth Audits:** Routinely inspect and revoke third-party OAuth 2.0 application access permissions.
