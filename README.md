# 🛡️ Harvard CS50 Cybersecurity — Course Notes

Personal study notes, threat models, cryptographic analysis, and lab documentation for Harvard University's **CS50 Cybersecurity**.

## 📚 Table of Contents
* [Week 1: Securing Accounts](#-week-1-securing-accounts)
* [Week 2: Securing Data](#-week-2-securing-data)

---

# 🔑 Week 1: Securing Accounts

### 📌 Overview
Academic notes, threat models, and mitigation strategies covering account security, authentication, password dynamics, and multi-factor authentication (MFA).

### 🎯 Threat Models & Attack Vectors
* **Brute-Force Attack:** Exhaustive computation testing all possible character permutations until valid credentials are discovered.
* **Dictionary Attack:** Targeted guessing using pre-compiled wordlists, cracked hash databases, and common password variations.
* **Credential Stuffing:** Automated replay of leaked username/password pairs from third-party breaches across unrelated services.
* **Phishing & Spear Phishing:** Deceptive communication designed to trick targets into submitting credentials on fake authentication portals.
* **SIM-Swapping:** Convincing mobile network operators to transfer a victim's phone number to an attacker's SIM, hijacking SMS-based 2FA.

### 🧠 Core Concepts
* **Authentication (AuthN):** Verifying identity (*"Who are you?"*).
* **Authorization (AuthZ):** Verifying permissions (*"What are you allowed to do?"*).
* **Password Entropy:** $E = L \times \log_2(R)$. Length ($L$) exponentially expands brute-force search space more effectively than character set size ($R$).
* **Multi-Factor Authentication (MFA):** Combining at least two distinct security factors:
  * *Something you know* (Password, PIN)
  * *Something you have* (TOTP app, Hardware key)
  * *Something you are* (Biometrics)

### 🛡️ Defenses & Best Practices
* Use zero-knowledge password managers (e.g., Bitwarden).
* Enforce TOTP or FIDO2 hardware keys over vulnerable SMS-based 2FA.
* Regularly audit OAuth third-party app permissions.

---

================================================================================

---

# 🔐 Week 2: Securing Data

### 📌 Overview
Personal notes covering data states, cryptographic primitives, key exchange protocols, applied security models, and future cryptographic threats.

---

## ⚙️ The Core Paradigm: Input, Algorithm & Output

In cybersecurity and cryptography, data transformation fundamentally follows Harvard CS50's core model: Input (Plaintext) passes through an Algorithm (Cipher/Function) to produce an Output (Ciphertext/Hash).

---

## 📌 Hashing, Salting & One-Way Functions

### 1. One-Way Hash Functions
Mathematical algorithms that convert input data of any size into a fixed-length output digest. They are strictly **one-way** — mathematically non-reversible.
* **Legacy Algorithms:** `MD5`, `SHA-1` (Deprecated due to hash collisions).
* **Modern Standard:** `SHA-256` (Used for data integrity verification).

### 2. Salting
Adding a unique, random string of characters (a salt) to a password before hashing.
* **Purpose:** Mitigates pre-computed lookup attacks (**Rainbow Tables**).
* **Dedicated Hashers:** `bcrypt` and `Argon2id` (automatic salting and key stretching).

---

## 📜 Cryptography Foundations

* **Cryptography:** The science of securing communications so only intended recipients can read data.
* **Codes vs. Ciphers:**
  * **Codes:** Substitute entire words/phrases with other symbols (*"Attack at dawn"* ➔ *"Blue Sky"*).
  * **Ciphers:** Algorithms that transform data character-by-character or bit-by-bit.
* **Encoding vs. Decoding:** Formatting data for transmission (e.g., Base64, ASCII). **Encoding is not encryption** — no secret key is used.
* **Plaintext, Encrypt & Decrypt:**
  * **Plaintext:** Readable data.
  * **Encryption:** Transforming plaintext into unreadable **Ciphertext** using a cipher and key (e.g., Caesar Cipher shifting letters by key $k$).
  * **Decryption:** Reversing ciphertext back to plaintext.

---

## 🔑 Key Systems & Cryptanalysis

### 1. Secret Key Cryptography (Symmetric Encryption)
Uses a **single shared key** for both encryption and decryption.
* **Pros:** Highly efficient for large datasets.
* **Cons:** Key distribution challenge — sharing secret keys safely across untrusted networks.
* **Standard:** `AES-256`.

### 2. Cryptanalysis
The practice of analyzing, cracking, or bypassing cryptographic schemes without possessing the secret key.

---

## 🌐 Public Key Cryptography & Key Exchange

### 1. Asymmetric Encryption Dynamics
Uses a mathematically linked key pair:
* **Public Key ($e, n$):** Shared openly; used to encrypt messages or verify signatures.
* **Private Key ($d, n$):** Kept strictly secret; used to decrypt ciphertext or sign hashes.

---

### 2. RSA Algorithm (Rivest–Shamir–Adleman)
RSA security relies on the computational difficulty of factoring the product of two extremely large prime numbers.

#### A. Key Generation Math
1. Select two large prime numbers $p$ and $q$.
2. Compute modulus $n$:
   $$n = p \times q$$
3. Calculate Euler's totient function $\phi(n)$:
   $$\phi(n) = (p - 1) \times (q - 1)$$
4. Choose a public exponent $e$ such that $1 < e < \phi(n)$ and $\gcd(e, \phi(n)) = 1$ (standard choice is $e = 65537$).
5. Compute private exponent $d$ as the modular multiplicative inverse of $e \pmod{\phi(n)}$:
   $$d \times e \equiv 1 \pmod{\phi(n)}$$

* **Public Key:** $(e, n)$
* **Private Key:** $(d, n)$

#### B. Encryption & Decryption Formulas
* **Encryption (Plaintext $m$ to Ciphertext $c$):**
  $$c = m^e \bmod n$$
* **Decryption (Ciphertext $c$ to Plaintext $m$):**
  $$m = c^d \bmod n$$

---

### 3. Diffie-Hellman Key Exchange (DHKE)
A mathematical protocol that allows two parties (Alice and Bob) to generate a shared secret key over an untrusted public network without transmitting the key itself.

#### A. Protocol Step-by-Step
1. **Public Domain Parameters:** Alice and Bob publicly agree on a large prime $p$ and generator $g$.
2. **Private Secrets:** Alice selects secret integer $a$; Bob selects secret integer $b$.
3. **Public Value Generation & Exchange:**
   * Alice computes and sends: 
     $$A = g^a \bmod p$$
   * Bob computes and sends: 
     $$B = g^b \bmod p$$

#### B. Shared Secret Proof
Alice and Bob compute the shared key $S$ independently:
* Alice computes: 
  $$S_{\text{Alice}} = B^a \bmod p = (g^b)^a \bmod p = g^{ab} \bmod p$$
* Bob computes: 
  $$S_{\text{Bob}} = A^b \bmod p = (g^a)^b \bmod p = g^{ab} \bmod p$$

Since $(g^b)^a \equiv (g^a)^b \equiv g^{ab} \pmod p$, both arrive at the **exact same shared secret key** $S$:
$$S = g^{ab} \bmod p$$

#### C. Security Hardness
An eavesdropper (Eve) intercepts $p$, $g$, $A$, and $B$. However, deriving the secret $a$ or $b$ to calculate $S$ requires solving the **Discrete Logarithm Problem (DLP)**:
$$a = \log_g(A) \bmod p$$
For sufficiently large primes (e.g., 2048-bit or 4096-bit), computing discrete logarithms is computationally infeasible using classical computers.

---

## 🔏 Identity, Signatures & Passkeys

* **Digital Signatures:** Sender encrypts a hash with their **Private Key**; recipients verify using the sender's **Public Key** (*Authenticity & Non-Repudiation*).
* **Passkeys:** Passwordless authentication using FIDO2/WebAuthn public-key standards and local biometrics.

---

## 🚚 Applied Data Protection States

* **Encryption in Transit:** Protecting active network data using **TLS 1.3** / HTTPS.
* **End-to-End Encryption (E2EE):** Encrypted on sender device, decrypted only on recipient device (e.g., Signal).
* **Encryption at Rest:** Protecting stored data on disk via **BitLocker**, **FileVault**, or **LUKS** (AES-256).
* **Secure Deletion:** Overwriting raw disk blocks with zeros/noise (zeroization) to prevent forensic recovery.

---

## ⚠️ Threats & Future Outlook

* **Ransomware:** Malware that locks local user files with strong encryption to extort ransom payments.
* **Quantum Computing Risk:** Future quantum hardware executing **Shor's Algorithm** will break current RSA and Diffie-Hellman schemes.
  * *Defense:* Migration to **Post-Quantum Cryptography (PQC)** standards.
