# Case 01 - Shopping / Allegro Phishing

| Field | Details |
| --- | --- |
| Case ID | PHISH-001 |
| Status | ✅ CONFIRMED PHISHING |
| Severity | HIGH |
| Source | PhishTank - Already Reported |
| My Role | Verification & Analysis (Not Initial Detection) |
| Date Analyzed | 17 Nov 2026 |
| Analyst | Awais Amjad |

**Malicious URL:** http://allegrolokalnie.letnie-okazje491831.shop/
**PhishTank ID:** 9560802
**Brand Impersonated:** Allegro Lokalnie (Polish Shopping Site)

---

## Executive Summary

This is a confirmed shopping phishing campaign impersonating Allegro Lokalnie. It was already reported on PhishTank. My work was to independently verify the report using VirusTotal, URLScan, and manual live-page inspection.

The attacker created a fake `.shop` domain that looked like the real Allegro site. The domain was only **2 HOURS old** at time of scan, while the real Allegro domains are **7-10 YEARS old**.

The page is now **DEAD**. After detection, the fake domain started redirecting to the real site and shows a 404 error. This is a classic short-lived phishing campaign - create, scam, then hide.

**Risk:** Users who visited during the active hours would have seen a fake Allegro login / payment page and could have lost account credentials and payment details.

---

## IoCs - Indicators of Compromise

| Indicator | Value |
| --- | --- |
| Fake Domain | allegrolokalnie.letnie-okazje491831.shop |
| Fake Subdomain | letnie-okazje491831.shop |
| Real Domain Impersonated | allegrolokalnie.pl |
| PhishTank IP | 5.134.215.224 |
| URLScan Main IP | 185.31.27.181 (Poland) |
| Other IP | 185.31.27.181 / 5.134.215.226 - QXL-POLAND |
| Cloudflare IP | 104.21.50.25 (Cloudflare) |
| Domain Age (Fake) | 2h old |
| Domain Age (Real) | 7yr old |

---

## 1. VirusTotal Result

**Score:** 4/93 vendors flagged
**Phishing:** Forcepoint, G-Data, SOCRadar, Sophos
**Suspicious:** ESET, LevelBlue

![](./Testing%20phishing%201%20in%20virustotal.png)

**Analysis:** 4 vendors flagged it as Phishing + 2 as Suspicious. Low score is normal for a 2-hour-old domain - most vendors had not seen it yet. This is why we do not rely on VirusTotal alone, we verify with URLScan + Domain Age.

---

## 2. URLScan.io Verification

**Submitted URL:** http://allegrolokalnie.letnie-okazje491831.shop/
**Effective URL:** https://allegrolokalnie.pl/o/
**Redirect:** Fake .shop domain -> Real allegrolokalnie.pl
**Main IP:** 185.31.27.181 (Poland)
**Main Domain Age:** 7 years old (Real site)
**Google Safe Browsing:** No classification for real domain
**Verdict:** No classification (Because site now redirects to real site)

![](./case%2001%20url.io%20scan%20result.png)

**What This Proves:**
Attacker used a fake .shop domain that looked like the real Allegro site.
When the fake domain was taken down / expired, it started redirecting to the real site.
This is a common evasion technique to hide phishing after detection.

---

## 3. Redirect Chain & IP Analysis

**Redirect Chain:**
1. http://allegrolokalnie.letnie-okazje491831.shop/ - HTTP 307
2. https://allegrolokalnie.letnie-okazje491831.shop/ - HTTP 302
3. https://allegrolokalnie.pl/o/ - Final Page

**Finding:** Attacker uses double redirect to hide phishing. First user lands on fake .shop domain, then redirected to look-alike .pl domain.

**IPs Found:**
- 104.21.50.25 (Cloudflare)
- 185.31.27.181 (QXL-POLAND)
- 5.134.215.226 (QXL-POLAND)

**Google Safe Browsing:** NO classification - Google has not flagged it yet, attack is new.
**Page Stats:** 99 Requests, 9 Domains

![](./case%2001%20url.io%20scan%20result%20part%202.png)

---

## 4. Live Page Verification (Manual Check)

**Status:** Page is DEAD / Taken Down

**Manual Check:**
- Opened fake URL in browser
- It redirected to: https://allegrolokalnie.pl/o/
- Result: 404 - "Ups, nic tu nie ma! / Page Not Found"

![](./case%201%20url.io%20given%20screenshot.png)

**What This Proves:**
The phishing page is now dead / taken down.
The attacker used a fake .shop domain to impersonate Allegro Lokalnie.
After detection, the domain now redirects to the real site and shows 404.
This confirms it was a short-lived phishing campaign.

---

## 5. Domain Age Analysis - SMOKING GUN

From URLScan.io Domains Tab:

| Domain | Age | Verdict |
| --- | --- | --- |
| allegrolokalnie.pl | 7yr old | REAL site |
| allegrostatic.com | 9yr old | REAL |
| allegroimg.com | 10yr old | REAL |
| letnie-okazje491831.shop | 2h old | FAKE / PHISHING |
| allegrolokalnie.letnie-okazje491831.shop | 2h old | FAKE / PHISHING |

![](./case%201%20domain%20detail%20url.io.png)

**Conclusion:**
The phishing domain was only 2 HOURS old at time of scan.
Legitimate Allegro domains are 7-10 YEARS old.
This huge age difference is the strongest indicator of phishing.
Attacker created a fresh domain, used it for a few hours, then redirected it to the real site to hide.

---

## Final Verdict: CONFIRMED PHISHING

**Confidence:** 100% - Verified by 3 independent methods (VirusTotal + URLScan + Domain Age + Live Page)

## Recommended Action
1. **Block Domain:** allegrolokalnie.letnie-okazje491831.shop / letnie-okazje491831.shop
2. **Block IPs:** 5.134.215.224, 185.31.27.181, 5.134.215.226, 104.21.50.25
3. **Monitor:** Watch for new .shop domains with "allegro" + "letnie-okazje" pattern

## MITRE ATT&CK Mapping
- **T1566.002 - Phishing: Spearphishing Link**
- **T1583.001 - Acquire Infrastructure: Domains**
- **T1204.001 - User Execution: Malicious Link**
- **T1071.001 - Application Layer Protocol: Web Protocols (Redirect Evasion)**