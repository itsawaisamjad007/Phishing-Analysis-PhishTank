# Case 04 - Netflix Upgrade Phishing (Netflix Impersonation)

| Field | Details |
| --- | --- |
| Case ID | PHISH-004 |
| Status | ✅ CONFIRMED PHISHING |
| Severity | HIGH |
| Source | PhishTank - Already Reported |
| My Role | Verification & Analysis (Not Initial Detection) |
| Date Analyzed | 18 Nov 2026 |
| Analyst | Awais Amjad |

- **Malicious URL:** https://www.netflix-upgrade.com/
- **Redirects To:** https://www.netflix-upgrade.com/pages/index.php
- **Domain:** www.netflix-upgrade.com
- **PhishTank ID:** 9561333
- **IP ADDRESS:** 79.133.42.33
- **Current Status Code:** 200 - LIVE
- **Category:** Phishing and Fraud

---

## Executive Summary

This is a confirmed phishing page impersonating Netflix. It uses the name "netflix-upgrade" to trick users into thinking they need to upgrade their Netflix account.

When opened, the main URL redirects to `/pages/index.php` - this is where the fake verification page is hosted. This redirect is a common trick to hide the real phishing page from simple checks.

The page is still **LIVE with Status 200**. Unlike Case 01 (404 - dead) and Case 03 (403 - blocked), this one is still active and dangerous.

**Risk:** Users who visit this page would see a fake Netflix verification page, complete the fake captcha, and then be taken to a fake login / payment page where they could lose their Netflix login + payment card details.

---

## IoCs - Indicators of Compromise

| Indicator | Value |
| --- | --- |
| Fake Domain | www.netflix-upgrade.com |
| Redirect URL | www.netflix-upgrade.com/pages/index.php |
| Main IP | 79.133.42.33 (Germany) |
| Second IP (IPv6) | 2a02:ec88:300:ed1a::2:b (United States - Wikimedia) |
| DNS A Record | 79.133.42.33 |
| ASN / Owner | AS214036 - ULTAHOST - Ultahost, Inc., US |
| TLS Certificate | Issued by YR1 on 16 Nov 2026, Valid for 3 Months |
| Domain Created | 17 Nov 2026, 01:29:12 (UTC) - Only 1 Day Old |
| Domain Registrar | Key-Systems GmbH |
| Status Code | 200 - LIVE |
| Content Type | text/html; charset=UTF-8 |
| Last Analysis | 22 hours ago (17 Nov 2026, 09:34:56 UTC) |

---

## 1. VirusTotal Result

- **Score:** 5/93 vendors flagged
- **Phishing:** ESET, Fortinet, Gridinsoft
- **Malicious:** Webroot, Seclookup

![](./case%204%20virustotal%20result.png)

- **Analysis:** Only 5 vendors flagged it, but these are strong vendors. ESET and Fortinet are both top-tier. Low detection does not mean safe - it means this is a new / low-profile phishing page that most vendors have not caught yet. This is why manual verification is important.

![](./case%204%20virustotal%20result%202.png)

- **Key Point:** Community Score is 5/93 - very low, which is typical for a fresh Netflix phishing campaign. In Case 03, 15 vendors flagged it because it was older. This one is only 1 day old, so detection is still low.

---

## 2. URLScan.io Result

- **Submitted URL:** https://www.netflix-upgrade.com/
- **Effective URL:** https://www.netflix-upgrade.com/pages/index.php

- **Summary:** This website contacted 3 IPs in 2 countries across 2 domains to perform 6 HTTP transactions. The main IP is 79.133.42.33, located in Germany and belongs to ULTAHOST-AS Ultahost, Inc., US. The main domain is www.netflix-upgrade.com.

- **TLS Certificate:** Issued by YR1 on November 16th 2026. (Valid for: 3mo.)

### Live Information:

**Current DNS A Record:** 79.133.42.33 (AS214036 - ULTAHOST-AS Ultahost, Inc., US)
**Domain Created:** November 17th 2026, 01:29:12 (UTC)
**Domain Registrar:** Key-Systems GmbH

![](./URL%20scan.io%201.png)

---

## 3. Domain & IP Information

| Domain | IP Address | Age | Verdict |
| --- | --- | --- | --- |
| netflix-upgrade.com | 79.133.42.33 | 1 Day Old (Created 17 Nov 2026) | FAKE / PHISHING |
| upload.wikimedia.org | 2a02:ec88:300:ed1a::2:b | 10yr old | REAL - Legit Image Hosting |

![](./url%20scan%20ip%20detail.png)

![](./url%20scan%20domain%20detail.png)

- **Finding:** The fake Netflix domain was created on 17 Nov 2026, only 1 day old. This is the biggest red flag. Real Netflix would never use a 1-day-old domain for account upgrades.

The second IP is Wikimedia's IPv6 address. The attacker is loading images (likely Netflix logo) from `upload.wikimedia.org` (10yr old, real site) to make the fake page look real.

- **Important Note:** The attacker is NOT impersonating `wikimedia.org`. That is a legitimate site. The attacker is just abusing it to host images for the fake Netflix page.

- **Note on Age:** URLScan shows "7yr old" next to netflix-upgrade.com in one view, but the Live Information clearly shows Domain Created: 17 Nov 2026. I am using the creation date from Live Information as the correct age, because that matches the VirusTotal first-seen date.

- **Page Statistics:** 6 HTTP Transactions, 3 IPs, 2 Countries, 2 Domains

---

## 4. Live Page Verification - Via URLScan.io

![](./live%20screenshot.png)

- **Note:** I did not open this link directly in my own browser. This screenshot is from URLScan.io's live scan. When URLScan opened the site with its scanner, it captured this fake verification page.

**What The Page Shows:**
- Netflix logo at the top to look real
- Heading: "Anti-Robot-Verifizierung | Netflix" in German
- Text: "Bitte verifizieren Sie, dass Sie kein Roboter sind, indem Sie dieses Cloudflare-Captcha lösen."
- A fake Cloudflare checkbox: "Verify you are human"
- A red button: "Überprüfen" (Verify)
- Footer: "Diese Seite ist durch Netflix-Sicherheitssysteme geschützt, um unbefugten Zugriff zu verhindern. © 2026 Netflix, Inc."

**What This Proves:**
1. Page is still LIVE with 200
2. Attacker is targeting German-speaking users - page is fully in German
3. Attacker is using a fake Cloudflare captcha to build trust before showing the fake login page
4. Real Netflix never uses a Cloudflare captcha on a separate "netflix-upgrade.com" domain - this is 100% fake
5. Redirect to /pages/index.php proves the phishing page is hidden behind a verification step

This is different from Case 01 (404 - dead), Case 02 (still LIVE - direct login), and Case 03 (403 - blocked). In this case the attacker is using a fake captcha gate to filter out bots and security scanners.

---

## Final Verdict: CONFIRMED PHISHING

**Confidence:** 100% - Verified by VirusTotal + URLScan + 1-Day-Old Domain + Redirect Behaviour + Fake Captcha Page

## Recommended Action
1. **Block Domain:** www.netflix-upgrade.com
2. **Block IP:** 79.133.42.33
3. **Report:** Report to Netflix Abuse + Google Safe Browsing for takedown
4. **Monitor:** Watch for new domains with "netflix-upgrade" + "netflix-verify" + "netflix-check" pattern

## MITRE ATT&CK Mapping
- **T1566.002 - Phishing: Spearphishing Link**
- **T1583.001 - Acquire Infrastructure: Domains**
- **T1204.001 - User Execution: Malicious Link**
- **T1566.001 - Phishing: Spearphishing Attachment (Fake Upgrade Email)**
- **T1036 - Masquerading: Match Legitimate Name or Location (Fake Captcha)**