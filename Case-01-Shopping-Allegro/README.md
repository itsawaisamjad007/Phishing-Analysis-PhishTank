# Case 01 - Shopping / Allegro Phishing

**URL:** http://allegrolokalnie.letnie-okazje491831.shop/
**PhishTank ID:** 9560802
**IP:** 5.134.215.224

## VirusTotal Result
- Score: 4/93 vendors flagged
- Forcepoint, G-Data, SOCRadar, Sophos = Phishing
- ESET, LevelBlue = Suspicious

## Screenshot:

![](./Testing%20phishing%201%20in%20virustotal.png)

-----

## Analysis - How I Identified It
1. Real site is allegro.pl, this is a long fake subdomain: allegrolokalnie.letnie-okazje491831.shop
2. Uses cheap .shop TLD, real shopping sites don't use this
3. Multiple redirects: Fake URL -> https://allegrolokalnie.pl/o/
4. 4 vendors on VirusTotal flagged it as Phishing

## Verdict: CONFIRMED PHISHING
## Recommended Action: Block Domain + Block IP

## URLScan.io Result

- Submitted URL: http://allegrolokalnie.letnie-okazje491831.shop/
- Effective URL: https://allegrolokalnie.pl/o/
- Redirect: Fake .shop domain -> Real allegrolokalnie.pl
- Main IP: 185.31.27.181 (Poland)
- Main Domain Age: 7 years old (Real site)
- Google Safe Browsing: No classification for real domain
- Verdict: No classification (Because site now redirects to real site)

## Screenshots 

![](./case%2001%20url.io%20scan%20result.png)

-----

## What This Proves
Attacker used a fake .shop domain that looked like the real Allegro site.
When the fake domain was taken down / expired, it started redirecting to the real site.
This is a common evasion technique to hide phishing after detection.


## Redirect Chain:

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

## Screenshots

![](./case%2001%20url.io%20scan%20result%20part%202.png)

## Live Page Verification (Manual Check)
- Opened fake URL in browser
- It redirected to: https://allegrolokalnie.pl/o/
- Result: 404 - "Ups, nic tu nie ma! / Page Not Found"

## Screenshot

![](./case%201%20url.io%20given%20screenshot.png)

## What This Proves
The phishing page is now dead / taken down.
The attacker used a fake .shop domain to impersonate Allegro Lokalnie.
After detection, the domain now redirects to the real site and shows 404.
This confirms it was a short-lived phishing campaign.


## Domain Age Analysis - SMOKING GUN

From URLScan.io Domains Tab:

| Domain | Age | Verdict |
| --- | --- | --- |
| allegrolokalnie.pl | 7yr old | REAL site |
| allegrostatic.com | 9yr old | REAL |
| allegroimg.com | 10yr old | REAL |
| letnie-okazje491831.shop | 2h old | FAKE / PHISHING |
| allegrolokalnie.letnie-okazje491831.shop | 2h old | FAKE / PHISHING |

## Screenshot

![](./case%201%20domain%20detail%20url.io.png)

## Conclusion
The phishing domain was only 2 HOURS old at time of scan.
Legitimate Allegro domains are 7-10 YEARS old.
This huge age difference is the strongest indicator of phishing.
Attacker created a fresh domain, used it for a few hours, then redirected it to the real site to hide.