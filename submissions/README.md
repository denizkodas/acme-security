---
name: Lab Submission
about: Submit your security incident lab analysis
title: '[SUBMISSION] Deniz Kodaş - Security Incident Lab'
labels: submission
assignees: ''
---

## 👤 Candidate Information

 Deniz Kodaş  
denizkodas.eng@gmail.com
https://www.linkedin.com/in/deniz-koda%C5%9F/
Istanbul, Türkiye  
09/11/2025  



## 📎 Submission Files

**Option A: Attached Files**
- Report PDF: ---[Deniz_Kodas_Acme_Security_Incident_Report (1).pdf](https://github.com/user-attachments/files/23442336/Deniz_Kodas_Acme_Security_Incident_Report.1.pdf)
- Video link: 

**Option B: External Links**
- Report: [Google Drive / Dropbox link]
- Video: [YouTube / Vimeo / Loom link]

---

## ⏱️ Time Tracking

**Total time spent:** ___ hours

**Breakdown:**
- Log analysis: ___ hours
- Architecture design: ___ hours
- Report writing: ___ hours
- Video creation: ___ hours

---

## 🎯 Summary

### Attack Vectors Identified
1. Phishing Campaign (Via E-mail) — Credential harvesting via spoofed domain: "acme-finance.com"
2. Web Application SQL Injection -  Malicious payloads through the "/dashboard/search" endpoint 
3. Mobile API Broken Access Control - 

### Key Findings
- Phishing Analysis: Around 09:00 AM on October 15, 2024, several employees received an email from security@acme-finance.com with the subject line “URGENT: Verify Your Account.”
Three employees  (user1, user3, and user5 ) clicked on the link in the message, which directed them to a malicious site hosted at "203.0.113.45".
All of these clicks came from the same external IP, which suggests that the phishing campaign was centrally controlled.
The timestamps of these clicks match the timing of unusual activity later seen in the web and API logs, including SQL injection payloads and mismatched token/user_id parameters.
Based on the correlation between these logs, it’s likely that the attacker used the harvested credentials from the phishing emails to launch follow-up attacks against the company’s web and API systems.

- Web Application Attack: Shortly after the phishing activity, the attacker logged into the system using credentials associated with user_id_ ;"1523".  
  From the same IP (203.0.113.45), they launched several SQL Injection attempts targeting "/dashboard/search" using payloads. The WAF blocked most of these requests, but at 09:23:45, one obfuscated payload (/*!50000OR*/ 1=1--) successfully bypassed filtering and returned a "200 OK" response code.  
  Afterward, the attacker requested "dashboard/export?format=csv", suggesting possible data extraction.


- Mobile API Exploitation: At around 2024-10-15 06:45:10, the same attacker IP (203.0.113.45) initiated a sequence of requests against the mobile API.
The attacker successfully logged in as user_id_ "1523" using the "/api/v1/login" endpoint.
Immediately after obtaining a valid session token (jwt_token_1523_stolen),
the attacker began accessing other users portfolio data by simply incrementing the account_id value in the request URL:
 "/api/v1/portfolio/1524 - ... - "/api/v1/portfolio/1538" All of these requests were accepted by the server with a 200 OK response and no access control or authorization validation was applied on the backend.
This indicates a Broken Access Control vulnerability, where the API trusted the client-provided account ID without verifying ownership against the authenticated user’s token.

### Top 3 Recommendations
1. Enforce SPF, DKIM, and DMARC to block spoofed sender domains and strengthen e-mail security.  
2. Implement parameterized queries and enhanced WAF filtering to prevent SQL Injection.  
3.  Add server-side authorization checks in API endpoints and implement rate limiting to prevent account enumeration.

---

## 🛠️ Tools Used

**Analysis:**
- Visual Studio 2022
- Excel 

**Diagrams:**
- draw.io

**Video:**
- 

**Other:**
- 

---

## ✅ Checklist

Please confirm:

- [X ] Report is max 5 pages
- [X ] Video is 10-15 minutes
- [ X] All log files were analyzed
- [ X] Timeline is timezone-corrected
- [X ] Framework mappings included (ISO 27001, NIST, OWASP)
- [X ] Architecture diagram included
- [X ] Video link is tested and working
- [X ] No plagiarism / proper attribution
- [X ] Original work, not AI-generated

---

## 💬 Optional Feedback

**What did you think of this lab?** 

Realistic and structured. It helped me connect phishing, web, and API vectors as part of a single attack chain.  


**Any suggestions for improvement?**

Correlation templates include a small hint about log formats


**Would you recommend this to others?**
- [ X] Yes

---

## 📧 Contact Preference

**Preferred contact method:**
- [ X] Email
- [X ] LinkedIn

**Best time to reach you:** 

09:00–18:00 Istanbul Time


---

## ⚖️ Declaration

I declare that this submission is my original work and I have followed all guidelines.

Deniz Kodaş  
09/11/2025  

---

_Thank you for your submission! We'll review it and get back to you within 1 week._
