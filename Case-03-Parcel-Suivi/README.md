# Case 03 - Canal Digital PJ Phishing (Portal Impersonation)

| Field | Details |
| --- | --- |
| Case ID | PHISH-003 |
| Status | ✅ CONFIRMED PHISHING |
| Severity | HIGH |
| Source | PhishTank - Already Reported |
| My Role | Verification & Analysis (Not Initial Detection) |
| Date Analyzed | 18 Nov 2026 |
| Analyst | Awais Amjad |

**Malicious URL:** https://portal.canaldigitalpj.com/pj/acesso-seguro...
**Domain:** portal.canaldigitalpj.com
**PhishTank ID:** 9561318
**IP ADDRESS:** 104.21.70.64
**Current Status Code:** 403 - Blocked
**Category:** Phishing and Fraud

---

## Executive Summary

This is a confirmed phishing page impersonating Canal Digital PJ portal. It was already reported on PhishTank. My work was to independently verify it using VirusTotal, URLScan, and live-page inspection.

This case is the strongest case so far. **15/94 vendors** flagged it, and even **Google Safe Browsing** marked it as **Malicious**.

The page is now **BLOCKED with 403**. When URLScan tried to open it live, it got a Cloudflare block page - "Sorry, you have been blocked". This means the attacker has now put a WAF block to hide the phishing content after detection.

**Risk:** Users who visited during active hours would have seen a fake "acesso-seguro" (secure access) login page and could have lost their portal credentials.

---

## IoCs - Indicators of Compromise

| Indicator | Value |
| --- | --- |
| Fake Domain | portal.canaldigitalpj.com |
| PhishTank IP | 104.21.70.64 |
| URLScan Main IP | 172.67.220.172 |
| DNS A Record | 188.114.96.3 |
| Location | Ascension Island |
| Owner / ASN | CLOUDFLARENET - Cloudflare, Inc., AS13335, US |
| TLS Certificate | Issued by WE1 on 16 Oct 2026, Valid for 3 Months |
| Domain Created | 18 Aug 2026, 07:23:33 (UTC) |
| Domain Registrar | Dominet (HK) Limited |
| Status Code | 403 - Blocked |
| Path Used | /pj/acesso-seguro... |

---

## 1. VirusTotal Result

- **Score:** 15/94 vendors flagged
- **Phishing:** alphaMountain.ai, BitDefender, Sophos, LevelBlue, Google Safe Browsing, ESET, Fortinet, Lionic, VIPRE, SOCRadar, Gridinsoft, G-Data, Forcepoint ThreatSeeker
- **Malicious:** Webroot, Seclookup

![](./case%203%20virustotal%20result.png)

- **Analysis:** 15 independent vendors flagged it as Phishing + Malicious. This was my own confirmation that the PhishTank report was correct, not a false positive.

![](./case%203%20virustotal%202.png)

- **Key Point:** Google Safe Browsing itself flagged it as Phishing. In Case 01 and Case 02, Google had not flagged it. In this case Google also flagged it, which means this is a confirmed, high-confidence phishing domain.

---

## 2. URLScan.io Result

- **Summary:** This website contacted 2 IPs in 1 country across 2 domains to perform 9 HTTP transactions. The main IP is 172.67.220.172, located in Ascension Island and belongs to CLOUDFLARENET (Cloudflare, Inc., US). The main domain is **portal.canaldigitalpj.com**.

- **TLS Certificate:** Issued by WE1 on October 16th 2026. (Valid for: 3mo).
- **Google Safe Browsing:** Malicious (for portal.canaldigitalpj.com)
- **Current DNS A Record:** 188.114.96.3 (AS13335 - CLOUDFLARENET - Cloudflare, Inc., US)
- **Domain Created:** August 18th 2026, 07:23:33 (UTC)
- **Domain Registrar:** Dominet (HK) Limited

![](./case%203%20urlscan.io%20result%201.png)

---

## 3. Domain & IP Information

| Domain | IP Address | Age | Verdict |
| --- | --- | --- | --- |
| portal.canaldigitalpj.com | 172.67.220.172 | ~3 Months Old (Created 18 Aug 2026) | FAKE / PHISHING |
| static.cloudflareinsights.com | 104.16.79.73 | 7yr old | REAL - Cloudflare Telemetry |

![](./case%203%20ip%20and%20domain%20info.png)

**Finding:** The fake portal domain was created on 18 Aug 2026, only ~3 months old. The only other domain in the chain is Cloudflare's own real telemetry domain (7yr old), which is used for analytics on all Cloudflare sites.

**Note:** The attacker is NOT impersonating `static.cloudflareinsights.com`. That is Cloudflare's legitimate tracking domain. The attacker is using Cloudflare hosting + Cloudflare protection to hide behind a trusted IP and make blocking harder.

**Page Statistics:** 9 HTTP Transactions, 2 IPs, 1 Country, 2 Domains

---

## 4. Live Page Verification

![](./Live%20page%20verification.png)

**What This Proves:**
1. The phishing page is no longer openly accessible
2. Attacker has enabled Cloudflare WAF / Bot Protection after detection
3. URLScan and normal users now get a 403 block page instead of the fake login page
4. This is a common post-detection evasion technique - block everyone to hide evidence

This is different from Case 01 (404 - dead) and Case 02 (still LIVE). In this case the attacker is actively hiding.

---

## Final Verdict: CONFIRMED PHISHING

**Confidence:** 100% - Verified by 3 independent methods (VirusTotal + URLScan + Live Page Block)

## Recommended Action
1. **Block Domain:** portal.canaldigitalpj.com
2. **Block IPs:** 104.21.70.64, 172.67.220.172, 188.114.96.3
3. **Report:** Already flagged by Google Safe Browsing, report to Cloudflare Abuse for takedown
4. **Monitor:** Watch for new subdomains with "canaldigitalpj" + "acesso-seguro" pattern

## MITRE ATT&CK Mapping
- **T1566.002 - Phishing: Spearphishing Link**
- **T1583.001 - Acquire Infrastructure: Domains**
- **T1204.001 - User Execution: Malicious Link**
- **T1071.001 - Application Layer Protocol: Web Protocols (Cloudflare Abuse)**
