# Case 02 - DBS Bank Loan Phishing (KTA Impersonation)

| Field | Details |
| --- | --- |
| Case ID | PHISH-002 |
| Status | ✅ CONFIRMED PHISHING |
| Severity | HIGH |
| Source | PhishTank - Already Reported |
| My Role | Verification & Analysis (Not Initial Detection) |
| Date Analyzed | 17 Nov 2026 |
| Analyst | Awais Amjad |

- **Malicious URL:** http://ktadbs-pinjaman.blogspot.com.br/?entity=3132...
- **Effective URL:** https://ktadbs-pinjaman.blogspot.com/?entity=3132...
- **Domain:** ktadbs-pinjaman.blogspot.com.br
- **PhishTank ID:** 9560676
- **Brand Impersonated:** DBS Bank - KTA (Kredit Tanpa Agunan)

---

## Executive Summary

This is a confirmed loan phishing page impersonating DBS Bank. It was already reported on PhishTank. My work was to independently verify the report using VirusTotal, URLScan, and manual live-page inspection.

The page is **still LIVE** and actively collecting victims via a personal Indonesian phone number. It abuses free Google Blogspot hosting to appear trustworthy, uses double redirects to hide its origin, and uses tracking tools to count victims.

**Risk:** Any user who contacts the number and shares ID / Credit Card details will face identity theft and financial fraud.

---

## IoCs - Indicators of Compromise

| Indicator | Value |
| --- | --- |
| Main IPv6 | 2a00:1450:4001:c17::84 |
| DNS A Record | 142.251.14.132 |
| Other IP | 142.250.115.132 (Google / Blogspot) |
| Location | Frankfurt am Main, Germany |
| Owner / ASN | GOOGLE - Google LLC, AS15169 |
| Suspicious IP | 167.114.174.44 - OVH SAS, AS16276, Canada |
| Cloudflare IP | 2606:4700:10::6814:883 - AS13335 |
| TLS Certificate | Issued by WE2 on 3 Nov 2026, Valid for 3 Months |
| Domain Age | 25d old (blogspot.com) / 2h old (.com.br) |
| Attacker Name | Yudha |
| Attacker Mobile | 0812 9098 6235 |
| Attacker Phone | 021 9098 6235 |

---

## 1. VirusTotal Result

- **Score:** 8/93 vendors flagged
- **Phishing:** alphaMountain.ai, BitDefender, Emsisoft, ESET, Fortinet, Lionic
- **Malicious:** Netcraft, Webroot

![](./case%202%20virustotal%20result.png)

- **Analysis:** 8 independent vendors flagged it as Phishing + Malicious. This was my first confirmation that the PhishTank report was correct, not a false positive.

---

## 2. URLScan.io Verification

- **Effective URL:** https://ktadbs-pinjaman.blogspot.com/?entity=3132...
- **Page Title:** KTA DBS | Kredit Tanpa Agunan ***INSTANT APPROVAL***
- **Domain Age:** 25d old at time of scan
- **TLS Certificate:** Issued by WE2 on November 3rd 2026, Valid for 3 months
- **Page Activity:** 9 IPs in 4 countries across 7 domains, 18 HTTP transactions
- **Scanned:** 13 times on URLScan already

![](./case%202%20url.io%20result%20part%201.png)

**Gap Found:**
- VirusTotal: 8/93 vendors flagged it
- Google Safe Browsing: No classification
- URLScan Verdict: No classification
- **Conclusion:** Google has not blocked its own Blogspot page yet. Attacker is abusing trusted Google infrastructure to bypass filters.

---

## 3. IP & ASN Analysis

**IP & ASN Information:**
- Main IPs: 2a00:1450:4001:c15::84, 2a00:1450:4001:c17::84 (GOOGLE - AS15169, Germany)
- Other IPs: 142.251.14.132, 142.251.20.191 (GOOGLE - AS15169, US)
- Suspicious IP: 167.114.174.44 (OVH SAS - AS16276, Canada) - Non-Google IP in chain
- Other IP: 2606:4700:10::6814:883 (CLOUDFLARENET - AS13335)

**Finding:** Most IPs belong to Google (AS15169), which is expected for Blogspot. But 1 IP belongs to OVH (Canada) and 1 to Cloudflare. This shows attacker is also using external infrastructure outside Google, possibly for tracking or redirect.

![](./case%202%20url.io%20IP%20details.png)

---

## 4. Redirect Chain & Domain Age Analysis

**Redirect Chain (Page URL History):**
1. http://ktadbs-pinjaman.blogspot.com.br/?entity=3132... - HTTP 307
2. https://ktadbs-pinjaman.blogspot.com.br/?entity=3132... - HTTP 302
3. https://ktadbs-pinjaman.blogspot.com/?entity=3132... - Final Page URL

**Finding:** Double redirect used. First from HTTP to HTTPS, then from .com.br to .com domain. This hides the original phishing link and makes tracking harder.

**Detected Technologies:**
- Blogger (Blogs) - Built on free Google Blogger platform
- Google Analytics (Analytics) - Attacker is tracking how many victims visit / click

![](./case%202%20url.io%20domain%20info.png)

**Domain Age Analysis - Strongest Proof:**

| Domain | Age | Verdict |
| --- | --- | --- |
| blogger.com | 10yr old | REAL - Google |
| google-analytics.com | 14yr old | REAL - Google |
| blogblog.com | 10yr old | REAL - Google |
| googleusercontent.com | 10yr old | REAL - Google |
| histats.com | 11yr old | REAL - Tracker |
| ktadbs-pinjaman.blogspot.com | 25d old | FAKE / PHISHING |
| ktadbs-pinjaman.blogspot.com.br | 2h old | FAKE / PHISHING |

**Conclusion:** All real Google domains are 10-14 years old. Only the attacker-created pinjaman subdomains are 25 days old and 2 hours old. This age difference confirms it is a freshly created phishing page abusing Blogspot.

**Third-Party Tracker Found:**
- histats.com (s10.histats.com / s4.histats.com) - 11yr old visitor counter
- Attacker uses Histats to count victims, common in loan phishing

**Page Statistics:** 18 Requests, 100% HTTPS, 70% IPv6, 7 Domains, 10 Subdomains, 9 IPs, 4 Countries, 265 kB Transfer, 790 kB Size, 15 Cookies

---

## 5. Live Page Verification (Manual Check)

**Status:** Page is LIVE, not taken down

**What The Page Shows:**
Page is in Indonesian, pretending to be DBS Bank's KTA (Kredit Tanpa Agunan) loan service.

**Fake Promises Used To Lure Victims:**
- "Konsultasikan Masalah Keuangan Anda, Saya Akan Proses Apply KTA Anda di Bank DBS, Sampai Anda Memperoleh Manfaat Dana Tunainya"
- "CEPAT prosesnya - MUDAH persyaratannya - PASTI hasilnya"
- Translation: "Fast process - Easy requirements - Guaranteed result"
- Claims loan can be used for: home renovation, school fees, wedding, holiday, business capital, electronics, etc.

**Attacker Contact Details Found On Page (IoCs):**
- Name Used: Yudha
- Mobile: 0812 9098 6235
- Phone: 021 9098 6235
- Claims to be: Marketing / Loan Advisor at Rumah DBS

**Fake Service Areas Listed:** JAKARTA, BOGOR, DEPOK, TANGERANG, BEKASI

**Fake Requirement Listed:**
- "SYARAT UTAMA MEMILIKI KARTU KREDIT"
- "Besar Pinjaman 5 juta sd. 200 juta"
- Translation: Main requirement is having a Credit Card, Loan amount 5 million to 200 million

![](./url.io%20live%20screenshot.png)

**Red Flags Found In Live Page:**
1. Real bank never uses a free Blogspot page for loans
2. Real bank never gives personal mobile number (0812...) as contact, uses official call center
3. Uses urgency and guarantee words - "PASTI hasilnya" (Guaranteed result) - real banks never guarantee loans
4. Page uses a person's name "Yudha" as loan officer, not official bank domain
5. Page still live despite being flagged by 8 vendors on VirusTotal - takedown not done yet

---

## Final Verdict: CONFIRMED PHISHING + MALICIOUS

**Confidence:** 100% - Verified by 3 independent methods (VirusTotal + URLScan + Live Page)

## Recommended Action
1. **Block Domain:** ktadbs-pinjaman.blogspot.com / ktadbs-pinjaman.blogspot.com.br
2. **Block IPs:** 2a00:1450:4001:c17::84, 142.251.14.132, 167.114.174.44
3. **Report:** Report to Google Safe Browsing to take down Blogspot page
4. **Block Number:** 0812 9098 6235 in fraud database

## MITRE ATT&CK Mapping
- **T1566.002 - Phishing: Spearphishing Link**
- **T1583.001 - Acquire Infrastructure: Domains**
- **T1204.001 - User Execution: Malicious Link**