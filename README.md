🚀 Step-by-Step Walkthrough – OWASP Top 10 (2025)

This section documents my approach to solving each vulnerability in the TryHackMe room.

---

## 🔎 1. Enumeration (Initial Step)

Before exploiting anything:

* Open the target website in browser
* Inspect pages using **Developer Tools (F12)**
* Check:

  * URLs and parameters
  * Forms (login, search, input fields)
  * Hidden endpoints
* Use tools like:

  * `view-source`
  * Burp Suite (intercept requests)

👉 Goal: Understand how the application works

---

## 🔓 2. Broken Access Control

**Objective:** Access restricted resources

### Steps:

1. Try accessing admin pages directly:

   ```
   /admin
   /dashboard
   /users
   ```
2. Modify URL parameters:

   ```
   ?id=1 → ?id=2
   ```
3. Check if authorization is enforced

👉 If access is granted without login → vulnerability found

---

## 🔐 3. Cryptographic Failures

**Objective:** Find sensitive data exposure

### Steps:

1. Check if site uses HTTP instead of HTTPS
2. Look for:

   * Plain text passwords
   * Weak hashing (e.g., MD5)
3. Decode/Crack hashes using:

   * Online hash crackers
   * `hash-identifier`

👉 Example: Cracking a weak password hash

---

## 💉 4. Injection (SQL Injection)

**Objective:** Manipulate database queries

### Steps:

1. Test input fields:

   ```
   ' OR 1=1 --
   ```
2. Try login bypass:

   ```
   admin' -- 
   ```
3. Use Burp Suite to modify requests

👉 If login bypass works → SQL Injection confirmed

---

## 🧱 5. Insecure Design

**Objective:** Identify logic flaws

### Steps:

1. Analyze workflow (login, reset password, etc.)
2. Try skipping steps
3. Test edge cases:

   * Access pages without completing previous steps

👉 Focus on how the system *should* behave vs actual behavior

---

## ⚙️ 6. Security Misconfiguration

**Objective:** Find improperly configured systems

### Steps:

1. Look for:

   * Default credentials (admin/admin)
   * Open directories (`/backup`, `/test`)
2. Check error messages:

   * Stack traces
   * Debug info

👉 Misconfigurations often leak sensitive info

---

## 📦 7. Vulnerable Components

**Objective:** Identify outdated libraries

### Steps:

1. Inspect page source
2. Identify versions:

   * JS libraries
   * Frameworks
3. Search vulnerabilities:

   ```
   "library version + exploit"
   ```

👉 Example: Old Log4j vulnerability

---

## 🔑 8. Authentication Failures

**Objective:** Break login systems

### Steps:

1. Try:

   * Weak passwords
   * Brute force (small wordlist)
2. Check:

   * No rate limiting
   * No account lockout

👉 Leads to unauthorized account access

---

## 🔄 9. Software & Data Integrity Failures

**Objective:** Exploit untrusted updates or inputs

### Steps:

1. Check file uploads
2. Try uploading:

   * Modified files
   * Malicious scripts
3. Look for insecure CI/CD or update mechanisms

👉 Example: Uploading a file that executes on server

---

## 📡 10. SSRF (Server-Side Request Forgery)

**Objective:** Force server to make requests

### Steps:

1. Find input fields that fetch URLs
2. Test with:

   ```
   http://localhost
   http://127.0.0.1
   ```
3. Try accessing internal services

👉 If server responds → SSRF confirmed

---

## 🧠 Final Approach

* Always start with **enumeration**
* Test **inputs and parameters**
* Think like an attacker:

  * “What happens if I change this?”
* Use **Burp Suite** for deeper testing

---

## 🎯 Key Learning

This room helped me understand:

* Real-world web vulnerabilities
* How to approach CTF challenges

# owasp-top-10-2025
This repository contains my learning and hands-on walkthrough of the OWASP Top 10 (2025) room on TryHackMe. The OWASP Top 10 is a globally recognized standard that highlights the most critical web application security risks.
