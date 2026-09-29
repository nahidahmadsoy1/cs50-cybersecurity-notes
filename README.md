# 🛡️ CS50 Cybersecurity Notes & Study Guide

> **Overview:** Comprehensive study notes, deep-dive concepts, and defensive principles covered throughout Harvard's **CS50's Introduction to Cybersecurity** course.

---

## 📋 Table of Contents
1. [Course Overview](#course-overview)
2. [Week 1: Introduction to Cybersecurity](#week-1-introduction-to-cybersecurity)
3. [Week 2: Securing Accounts & Identity](#week-2-securing-accounts--identity)
4. [Week 3: Securing Data & Cryptography](#week-3-securing-data--cryptography)
5. [Week 4: Securing Software](#week-4-securing-software)
6. [Technologies & Tools](#technologies--tools)

---

## Course Overview

This repository serves as a personal academic knowledge base documenting my learning journey through Harvard's CS50 Cybersecurity course. It covers network defense, authentication models, cryptographic systems, software vulnerabilities, and defensive engineering practices.

---

## Week 1: Introduction to Cybersecurity

### 📌 Core Principles
* **CIA Triad:**
  * **Confidentiality:** Ensuring data is accessible only to authorized entities.
  * **Integrity:** Maintaining the accuracy, completeness, and uncorrupted state of data.
  * **Availability:** Ensuring systems and data are accessible when needed by authorized users.

### 🌐 Threat Vectors & Infrastructure
* **Threat Actors:** Adversaries ranging from script kiddies and insider threats to organized cybercrime groups and advanced persistent threats (APTs).
* **IP Addresses & Routing:** How internet communication protocols route packets and where interception risks exist.
* **Firewalls & Network Segmentation:** Filtering incoming/outgoing traffic based on security rules to isolate sensitive environments.

---

## Week 2: Securing Accounts & Identity

### 🔑 Authentication Models
* **Three Authentication Factors:**
  1. *Something you know:* Passwords, PINs, passphrases.
  2. *Something you have:* Security keys (YubiKey), authenticator apps (TOTP), SMS tokens.
  3. *Something you are:* Biometrics (fingerprint scan, facial recognition, iris scan).
* **Multi-Factor Authentication (MFA):** Requiring two or more distinct factors to prevent unauthorized entry even if credentials are compromised.

### 🛡️ Credential Protection
* **Password Hashing:** Storing one-way mathematical hashes instead of plaintext passwords.
* **Salting:** Adding random unique strings to passwords before hashing to defeat precomputed lookup attacks (Rainbow Tables).
* **Attack Vectors:** Mitigating brute-force attempts, credential stuffing, and dictionary attacks through rate-limiting and lockout policies.

---

## Week 3: Securing Data & Cryptography

### 🔒 Cryptographic Foundations
* **Symmetric Encryption:** Uses a single shared secret key for both encryption and decryption (e.g., AES-256). Fast and ideal for bulk data.
* **Asymmetric Encryption:** Uses a mathematically linked key pair: a **Public Key** for encryption and a **Private Key** for decryption (e.g., RSA, ECC).

### ✍️ Integrity & Secure Protocols
* **Cryptographic Hash Functions:** Algorithms like SHA-256 that produce fixed-size outputs to verify file integrity.
* **Digital Signatures:** Combining asymmetric encryption with hashing to ensure non-repudiation and sender authenticity.
* **Transport Layer Security (TLS/HTTPS):** Encrypting data in transit over public networks using public key infrastructure (PKI) and SSL certificates.
* **Virtual Private Networks (VPNs):** Creating encrypted tunnels to shield network traffic on untrusted networks.

---

## Week 4: Securing Software

### ⚠️ Memory Safety & Vulnerabilities
* **Buffer Overflow:** Occurs when a program writes beyond its allocated memory boundary, potentially corrupting adjacent memory or allowing arbitrary code execution.
* **C/C++ Memory Management:** Understanding how manual pointer arithmetic and lack of bound checking lead to exploitable security flaws.

### 💉 Injection Attacks & Sanitization
* **Input Validation & Sanitization:** Treating all external user input as untrusted. Sanitizing strips harmful characters, while validation confirms format compliance.
* **SQL Injection (SQLi):** Malicious inputs altering backend database queries.
  * **Prevention:** Utilizing **Parameterized Queries (Prepared Statements)** to separate SQL execution logic from data inputs.
* **Cross-Site Scripting (XSS):** Injecting client-side scripts into web pages viewed by other users.
  * **Prevention:** Context-aware output encoding and enforcing strict Content Security Policies (CSP).

### 🛡️ Defensive Engineering Practices
* **Principle of Least Privilege (PoLP):** Granting system processes and user accounts only the minimal access rights necessary to perform their functions.
* **Code Audits & Dependency Management:** Regularly scanning source code and third-party libraries for known software vulnerabilities (CVEs).

---

## Technologies & Tools

* **Academic Platform:** Harvard University (CS50)
* **Domains Covered:** Systems Security, Web Application Security, Cryptography, Identity Management
* **Version Control:** Git & GitHub
