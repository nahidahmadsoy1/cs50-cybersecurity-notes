# cs50-cybersecurity-notes
Comprehensive notes, threat models, and labs for Harvard CS50 Cybersecurity.
---

## 🔒 Week 1: Securing Accounts

### 📌 Overview
Notes and key security models covering authentication, credential safety, password entropy, and multi-factor authentication (MFA) mechanisms.

---

### 🔑 Core Concepts

#### 1. Authentication vs. Authorization
* **Authentication (AuthN):** Verifying identity (*Who are you?*).
* **Authorization (AuthZ):** Verifying permissions (*What are you allowed to do?*).

#### 2. Password Entropy & Strength
* **Definition:** A mathematical measurement of unpredictability in a password.
* **Key Takeaway:** Length beats complexity. Increasing password length exponentially expands the brute-force attack search space.

#### 3. Multi-Factor Authentication (MFA)
Authentication factors must combine at least two distinct categories:
* **Something you know:** Password, PIN, security questions.
* **Something you have:** Authenticator app (TOTP), physical YubiKey, SMS code.
* **Something you are:** Fingerprint, facial recognition, biometrics.

---

### 🛡️ Key Defenses & Best Practices
* Use a trusted password manager (e.g., Bitwarden, 1Password) to generate unique, high-entropy passphrases.
* Avoid SMS-based 2FA where possible due to SIM-swapping risks; prefer TOTP apps or FIDO2 hardware keys.
* Perform regular account security audits and revoke unused third-party OAuth access.
