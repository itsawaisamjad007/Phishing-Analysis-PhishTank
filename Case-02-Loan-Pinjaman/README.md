# Case 02 - Loan / Pinjaman Phishing

**URL:** http://ktadbs-pinjaman.blogspot.com.br/?entity=3132...
**Domain:** ktadbs-pinjaman.blogspot.com.br
**IP:** 142.250.115.132 (Google / Blogspot)

## VirusTotal Result
- Score: 8/93 vendors flagged
- Phishing: alphaMountain.ai, BitDefender, Emsisoft, ESET, Fortinet, Lionic
- Malicious: Netcraft, Webroot

## Screenshot 
![](./case%202%20virustotal%20result.png)

----
## Analysis - How I Identified It

This URL was already listed on PhishTank. I verified it independently using VirusTotal to increase my phishing analyzing skill.

## Verdict: CONFIRMED PHISHING + MALICIOUS
## Recommended Action: Block Domain + Report to Google Safe Browsing

## URLScan.io Result

**Effective URL:** https://ktadbs-pinjaman.blogspot.com/?entity=3132...
**PhishTank ID:** 9560676

**Main IP:** 2a00:1450:4001:c17::84
**DNS A Record:** 142.251.14.132
**Location:** Frankfurt am Main, Germany
**Owner:** GOOGLE - Google LLC, US

## 1. URLScan.io Verification

**Domain Age:** 25d old at time of scan
**TLS Certificate:** Issued by WE2 on November 3rd 2026, Valid for 3 months
**Page Activity:** 9 IPs in 4 countries across 7 domains, 18 HTTP transactions
**Scanned:** 13 times on URLScan already

**Page Title:** KTA DBS | Kredit Tanpa Agunan ***INSTANT APPROVAL***

## Screenshot

![](./case%202%20url.io%20result%20part%201.png)

**IP & ASN Information:**

- Main IPs: 2a00:1450:4001:c15::84, 2a00:1450:4001:c17::84 (GOOGLE - AS15169, Germany)
- Other IPs: 142.251.14.132, 142.251.20.191 (GOOGLE - AS15169, US)
- Suspicious IP: 167.114.174.44 (OVH SAS - AS16276, Canada) - Non-Google IP in chain
- Other IP: 2606:4700:10::6814:883 (CLOUDFLARENET - AS13335)

**Finding:** Most IPs belong to Google (AS15169), which is expected for Blogspot. But 1 IP belongs to OVH (Canada) and 1 to Cloudflare. This shows attacker is also using external infrastructure outside Google, possibly for tracking or redirect.

![](./case%202%20url.io%20IP%20details.png)

---
**Redirect Chain (Page URL History):**
1. http://ktadbs-pinjaman.blogspot.com.br/?entity=3132... - HTTP 307
2. https://ktadbs-pinjaman.blogspot.com.br/?entity=3132... - HTTP 302
3. https://ktadbs-pinjaman.blogspot.com/?entity=3132... - Final Page URL

**Finding:** Double redirect used. First from HTTP to HTTPS, then from .com.br to .com domain. This hides the original phishing link and makes tracking harder.

**Detected Technologies:**
- Blogger (Blogs) - Built on free Google Blogger platform
- Google Analytics (Analytics) - Attacker is tracking how many victims visit / click


![](./case%202%20url.io%20domain%20info.png)
---
### Live Page Content

- Page is LIVE, not dead
- Title: Kredit Tanpa Agunan / Pinjaman Online
- Promise: Easy application, fast process, no collateral, fast approval
- Language: Indonesian, targets Indonesian loan seekers

![](./url.io%20live%20screenshot.png)
