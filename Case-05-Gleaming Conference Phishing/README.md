# Case 05 - Gleaming Conference Phishing (Framer Abuse)

| Field | Details |
| --- | --- |
| Case ID | PHISH-005 |
| Status | ✅ CONFIRMED PHISHING |
| Severity | HIGH |
| Source | PhishTank - Already Reported |
| My Role | Verification & Analysis (Not Initial Detection) |
| Date Analyzed | 19 Nov 2026 |
| Analyst | Awais Amjad |

- **Malicious URL:** https://gleaming-conference-764748.framer.app/
- **Domain:** gleaming-conference-764748.framer.app
- **PhishTank ID:** 9561836
- **IP ADDRESS:** 31.43.161.6
- **Current Status Code:** 404 - DEAD
- **Category:** Phishing and Fraud

---

## Executive Summary

This is a confirmed phishing page hosted on Framer (framer.app). The attacker abused Framer's free website builder to create a fake "Gleaming Conference" page.

The page is now **DEAD with Status 404**. Like Case 01, it was taken down after detection. But VirusTotal still shows a very high detection score, which proves it was real phishing.

**Risk:** During its active hours, users who visited this page would have seen a fake conference / event page designed to steal login or payment details.

---

## IoCs - Indicators of Compromise

| Indicator | Value |
| --- | --- |
| Fake Domain | gleaming-conference-764748.framer.app |
| IP Address | 31.43.161.6 |
| Status Code | 404 - DEAD |
| Content Type | text/html; charset=utf-8 |
| Last Analysis | 3 hours ago (19 Nov 2026, 00:39:13 UTC) |

---

## 1. VirusTotal Result

- **Score:** 19/94 vendors flagged
- **Phishing:** alphaMountain.ai, BitDefender, Cluster25, CyRadar, DNS8, Emsisoft, ESET, Forcepoint - - - ThreatSeeker, Fortinet, G-Data, Gridinsoft, Kaspersky, Lionic, Rising, SOCRadar, Sophos, VIPRE
- **Malicious:** Netcraft, URLQuery
- **Not Recommended:** Ermes

![](./virustotal%20result%201.png)  

**Analysis:** 19 vendors flagged it - this is the highest score so far. Case 03 had 15, Case 04 had only 5. This one has 19, including Kaspersky, BitDefender, ESET, Fortinet, Sophos - all top-tier vendors. This is not a false positive.

**Key Point:** Even though the page is now 404 dead, 19 vendors still flag it. This proves the takedown happened after it was already caught.

---

## 2. URLScan.io Result

**Submitted URL:** https://gleaming-conference-764748.framer.app/
**Scanned From:** DE - 19 Nov 2026, 4:23:10 am UTC

**Summary:** This website contacted 2 IPs in 2 countries across 2 domains to perform 3 HTTP transactions. The main IP is 31.43.160.6, located in Ascension Island and belongs to AMAZON-02 - Amazon.com, Inc., US. The main domain is gleaming-conference-764748.framer.app. (20h old)

**TLS Certificate:** Issued by YE1 on October 2nd 2026. (Valid for: 3mo.)

### Live Information:

**Google Safe Browsing:** Malicious for gleaming-conference-764748.framer.app
**Current DNS A Record:** 31.43.160.6 (AS16509 - AMAZON-02 - Amazon.com, Inc., US)

![](./url%20scan.io%201.png)
---

## 3. Domain & IP Information

### IP Detail

| IP Address | Location | ASN / Owner | Domain | Verdict |
| --- | --- | --- | --- | --- |
| 31.43.160.6 | Ascension Island | AS16509 - AMAZON-02 - Amazon.com, Inc., US | gleaming-conference-764748.framer.app - 20h old - PTR: sites.framer.app | FAKE / PHISHING |
| 2600:9000:208a:6200:d:6b42:4ec0:93a1 | United States | AS16509 - AMAZON-02 - Amazon.com, Inc., US | app.framerstatic.com - 6yr old | REAL - Framer Legit Static Hosting 

![](./url%20scan.io%201.png)

### Domains Detail

| Apex Domain | Subdomain | Age / Rank | Transfer | Verdict |
| --- | --- | --- | --- | --- |
| framer.app | gleaming-conference-764748.framer.app | 20h old | 5 KB | FAKE / PHISHING |
| framerstatic.com | app.framerstatic.com | 6yr old - Cisco Umbrella Rank: 33301 | 98 KB | REAL - Framer Legit |

![](./url%20scan%20domain%20info.png)

**Finding:** The fake domain is only 20 hours old. Its PTR record is `sites.framer.app`, which confirms it was hosted on Framer's own infrastructure.

The second domain is Framer's real static hosting `app.framerstatic.com` (6yr old, Cisco Umbrella Rank 33301). This is used by all Framer sites to load CSS, JS and images. It is legitimate. The transfer size proves it - 98 KB came from the real Framerstatic, while only 5 KB came from the fake page because it was already deleted.

**Important Note:** The attacker is NOT impersonating Amazon or Framerstatic. Amazon is just the hosting provider (Framer runs on Amazon), and Framerstatic is Framer's own real domain. The attacker abused Framer's free website builder to create the fake conference page.

**Page Statistics:** 3 HTTP Transactions, 2 IPs, 2 Countries, 2 Domains


---

## 4. Live Page Verification - Via URLScan.io

![](./url%20scan%20live%20screenshot%20.png)


**What This Proves:**
1. Page is now DEAD with 404
2. Framer itself has removed the phishing page - this is why it shows "Site Not Found"
3. URLScan's screenshot proves the takedown, not just VirusTotal's 404
4. Google Safe Browsing still marks it as Malicious, which means Google caught it before takedown

This is same as Case 01 (404 - dead) but different from Case 03 (403 - blocked) and Case 04 (200 - live with fake captcha). In this case the platform itself (Framer) took it down.

---

## Final Verdict: CONFIRMED PHISHING

**Confidence:** 100% - Verified by VirusTotal (19/94) + URLScan + Google Safe Browsing Malicious + 20h Old Domain + Framer Takedown

## Recommended Action
1. **Block Domain:** gleaming-conference-764748.framer.app
2. **Block IPs:** 31.43.160.6, 31.43.161.6
3. **Report:** Report to Framer Abuse for takedown - already dead
4. **Monitor:** Watch for new subdomains with "gleaming-conference" + "framer.app" pattern

## MITRE ATT&CK Mapping
- **T1566.002 - Phishing: Spearphishing Link**
- **T1583.001 - Acquire Infrastructure: Domains**
- **T1204.001 - User Execution: Malicious Link**
- **T1583.006 - Acquire Infrastructure: Web Services (Framer Abuse)**