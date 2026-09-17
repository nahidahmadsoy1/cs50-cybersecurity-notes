# CS50 Cybersecurity — Week 1: Securing Accounts

## 📌 Overview
Academic notes, threat models, and mitigation strategies covering account security, authentication, password dynamics, and multi-factor authentication (MFA).

---

## 🎯 Threat Models & Attack Vectors

### 1. Credential & Password Attacks
* **Brute-Force Attack:** Systematically guessing every possible combination of characters until the correct credential is found.
* **Dictionary Attack:** Attempting pre-compiled lists of common words, leaked passwords, and known variation patterns.
* **Credential Stuffing:** Automated testing of stolen username/password pairs across multiple unrelated websites.

### 2. Social Engineering & Interception
* **Phishing:** Deceptive attempts via forged emails or malicious portals to trick users into handing over authentication credentials.
* **SIM-Swapping:** Fraudulently convincing a mobile network operator to transfer a victim's phone number to an attacker's SIM card to bypass SMS-based 2FA.

---

## 🔑 Core Concepts

### 1. Authentication vs. Authorization
* **Authentication (AuthN):** Verifying identity (*Who are you?*).
* **Authorization (AuthZ):** Verifying permissions (*What are you allowed to do?*).

### 2. Password Entropy & Dynamics
* **Definition:** A mathematical measurement of unpredictability in a password.
* **Key Takeaway:** Length beats complexity. Increasing password length exponentially expands the brute-force search space.

### 3. Multi-Factor Authentication (MFA)
Authentication factors must combine at least two distinct categories:
* **Something you know:** Passwords, PINs, passphrase.
* **Something you have:** Authenticator apps (TOTP), physical FIDO2 hardware keys (YubiKey).
* **Something you are:** Biometrics (Fingerprint, Facial Recognition).

---

## 🛡️ Key Defenses & Best Practices
* Deploy high-entropy passphrases using reliable password managers (e.g., Bitwarden).
* Enforce TOTP or FIDO2 hardware keys over SMS-based 2FA to mitigate SIM-swapping attack vectors.
* Perform regular account security audits and revoke unneeded third-party OAuth permissions.
