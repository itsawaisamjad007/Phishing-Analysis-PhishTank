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
- **IP ADDRESS:** 31.43.160.6 (URLScan) / 31.43.161.6 (VirusTotal)
- **Current Status Code:** 404 - DEAD
- **Category:** Phishing and Fraud

---

## Executive Summary

This one was hosted on Framer. The attacker just used Framer's free website builder and made a fake "Gleaming Conference" page.

Now the page is **404 - DEAD**. Same as Case 01, it got taken down after detection. But VirusTotal still shows 19 vendors flagging it, so it was clearly real phishing, not a false positive.

**Risk:** When it was live, anyone who opened it would have seen a fake conference page, and from there their login or payment details could have been stolen.

---

## IoCs - Indicators of Compromise

| Indicator | Value |
| --- | --- |
| Fake Domain | gleaming-conference-764748.framer.app |
| Main IP (URLScan) | 31.43.160.6 (Ascension Island) |
| IP (VirusTotal) | 31.43.161.6 |
| Second IP (IPv6) | 2600:9000:208a:6200:d:6b42:4ec0:93a1 (United States) |
| ASN / Owner | AS16509 - AMAZON-02 - Amazon.com, Inc., US |
| PTR Record | sites.framer.app |
| TLS Certificate | Issued by YE1 on 2 Oct 2026, Valid for 3 Months |
| Domain Age | 20h old - Only 20 Hours Old |
| Status Code | 404 - DEAD |
| Content Type | text/html; charset=utf-8 |
| Last Analysis | 3 hours ago (19 Nov 2026, 00:39:13 UTC) |
| Google Safe Browsing | Malicious for gleaming-conference-764748.framer.app |

---

## 1. VirusTotal Result

- **Score:** 19/94 vendors flagged
- **Phishing:** alphaMountain.ai, BitDefender, Cluster25, CyRadar, DNS8, Emsisoft, ESET, Forcepoint -  - - ThreatSeeker, Fortinet, G-Data, Gridinsoft, Kaspersky, Lionic, Rising, SOCRadar, Sophos, VIPRE
- **Malicious:** Netcraft, URLQuery
- **Not Recommended:** Ermes

![](./virustotal%20result%201.png)

This is the highest score so far. Case 03 had 15, Case 04 had only 5, and this one has 19. And it was caught by big names like Kaspersky, BitDefender, ESET, Fortinet, Sophos. So there is no doubt here.

One more thing, the page is already 404 dead but still 19 vendors are flagging it. That means it was caught first, then taken down.

---

## 2. URLScan.io Result

- **Submitted URL:** https://gleaming-conference-764748.framer.app/
- **Scanned From:** DE - 19 Nov 2026, 4:23:10 am UTC

- **Summary:** This website contacted 2 IPs in 2 countries across 2 domains to perform 3 HTTP transactions. The main IP is 31.43.160.6, located in Ascension Island and belongs to AMAZON-02 - Amazon.com, Inc., US. The main domain is gleaming-conference-764748.framer.app. (20h old)

- **TLS Certificate:** Issued by YE1 on October 2nd 2026. (Valid for: 3mo.)

### Live Information:

- **Google Safe Browsing:** Malicious for gleaming-conference-764748.framer.app
- **Current DNS A Record:** 31.43.160.6 (AS16509 - AMAZON-02 - Amazon.com, Inc., US)

![](./url%20scan.io%201.png)

---

## 3. Domain & IP Information

### IP Detail

| IP Address | Location | ASN / Owner | Domain | Verdict |
| --- | --- | --- | --- | --- |
| 31.43.160.6 | Ascension Island | AS16509 - AMAZON-02 - Amazon.com, Inc., US | gleaming-conference-764748.framer.app - 20h old - PTR: sites.framer.app | FAKE / PHISHING |
| 2600:9000:208a:6200:d:6b42:4ec0:93a1 | United States | AS16509 - AMAZON-02 - Amazon.com, Inc., US | app.framerstatic.com - 6yr old | REAL - Framer Legit Static Hosting |


### Screenshot 

![](./url%20scan.io%20ip%20info.png)

### Domains Detail

| Apex Domain | Subdomain | Age / Rank | Transfer | Verdict |
| --- | --- | --- | --- | --- |
| framer.app | gleaming-conference-764748.framer.app | 20h old | 5 KB | FAKE / PHISHING |
| framerstatic.com | app.framerstatic.com | 6yr old - Cisco Umbrella Rank: 33301 | 98 KB | REAL - Framer Legit |

### Screenshot

![](./url%20scan%20domain%20info.png)

The biggest point here is that the fake domain was only 20 hours old. And its PTR is `sites.framer.app`, which confirms it was hosted on Framer's own servers.

The second domain `app.framerstatic.com` is 6 years old and has a Cisco Umbrella Rank of 33301. That is Framer's real domain where all the CSS / JS / images load from. That one is fully legit.

You can also see it from the transfer size. Only 5 KB came from the fake page because it was already deleted, and 98 KB came from the real Framerstatic.

**Important Note:** The attacker is NOT impersonating Amazon or Framerstatic. Amazon is just the hosting provider, Framer runs on Amazon. The real abuse was done on Framer's free builder.

**Page Statistics:** 3 HTTP Transactions, 2 IPs, 2 Countries, 2 Domains

---

## 4. Live Page Verification - Via URLScan.io

![](./url%20scan%20live%20screenshot%20.png)

**Note:** I did not open this link in my own browser. This screenshot is from URLScan.io's live scan.

**What The Page Shows:**
- Page Title: "Site Not Found | Framer"
- Just a blank white page with a small Framer logo in the middle
- No conference content left at all

**What This Proves:**
1. Page is now DEAD with 404
2. Framer itself deleted this phishing page, that is why it shows "Site Not Found"
3. It is not just VirusTotal saying 404, the URLScan screenshot also confirms the takedown
4. Google Safe Browsing still marks it as Malicious, which means Google caught it before the takedown

This is same as Case 01 (404 - dead) but different from Case 03 (403 - blocked) and Case 04 (200 - live with fake captcha). In this case the platform itself took it down.

---

## Final Verdict: CONFIRMED PHISHING

**Confidence:** 100% - Verified by VirusTotal (19/94) + URLScan + Google Safe Browsing Malicious + 20h Old Domain + Framer Takedown

## Recommended Action
1. **Block Domain:** gleaming-conference-764748.framer.app
2. **Block IPs:** 31.43.160.6, 31.43.161.6
3. **Report:** Report to Framer Abuse - already dead
4. **Monitor:** Watch for new subdomains with "gleaming-conference" + "framer.app" pattern

## MITRE ATT&CK Mapping
- **T1566.002 - Phishing: Spearphishing Link**
- **T1583.001 - Acquire Infrastructure: Domains**
- **T1204.001 - User Execution: Malicious Link**
- **T1583.006 - Acquire Infrastructure: Web Services (Framer Abuse)**