# Phishing Analysis - PhishTank (5 Cases)

## Project Objective
I collected 5 different phishing URLs from PhishTank, analyzed them using VirusTotal, URLScan.io and Whois Lookup, and compared their techniques.

## Tools Used
- PhishTank - To collect live phishing URLs
- VirusTotal - To check URL detection
- URLScan.io - To view page safely without opening it
- Whois Lookup - To check domain creation date

## Comparison Table

| Case | Type | Domain | VirusTotal Score | Status Code | Verdict |
| --- | --- | --- | --- | --- | --- |
| Case 01 | Shopping / Fake Shop | allegrolokalnie.letnie-okazje491831.shop |  4/93 | 404 - DEAD | CONFIRMED PHISHING |
| Case 02 | Login / Direct Login | ktadbs-pinjaman.blogspot.com.br | 8/94 | 200 - LIVE | CONFIRMED PHISHING |
| Case 03 | Parcel / Fake Tracking | portal.canaldigitalpj.com | 15/94 | 403 - BLOCKED | CONFIRMED PHISHING |
| Case 04 | Netflix / Fake Upgrade | www.netflix-upgrade.com | 5/93 | 200 - LIVE | CONFIRMED PHISHING |
| Case 05 | Conference / Framer Abuse | gleaming-conference-764748.framer.app | 19/94 | 404 - DEAD | CONFIRMED PHISHING |

## Key Findings :

1. **Low detection does not mean safe:** Case 04 had only 5/93 detections but was 100% live phishing with a fake German captcha page. It was just too new.
2. **High detection means it was already caught:** Case 05 had 19/94 detections, the highest in this project. Kaspersky, BitDefender, ESET, Fortinet, Sophos all flagged it.
3. **Attackers abuse free platforms:** Case 05 was built on Framer's free builder. No need to buy hosting, just make a subdomain and start phishing.
4. **Fake captcha is used as a filter:** Case 04 used a fake Cloudflare captcha to build trust and to filter out bots and scanners before showing the fake login.
5. **Age is the biggest red flag:** Case 04 domain was only 1 day old, Case 05 was only 20 hours old. Real brands never use 1-day-old domains.
6. **Status tells the story:** 2 cases were already dead (404), 1 was blocked (403), and 2 were still live (200). Takedown is slow, so manual verification matters.
7. **Legit services are abused for trust:** Case 04 loaded images from Wikimedia, Case 05 loaded files from Framerstatic. Attackers use real domains to make fake pages look real.

## How I Verified (Safe Method)
I did not open any phishing link directly in my own browser. I used VirusTotal and URLScan.io screenshots for for domain and IP confirmation amd for live page verification.

## Indicators of Compromise (IoCs)
All IoCs are listed in `IoCs.txt`.

## Analyst
Awais Amjad - SOC Level 1 Aspirant
Date: 17-19 Nov 2026


## Project Structure

```
Phishing-Analysis-PhishTank/
├── README.md
├── IoCs.txt
├── Screenshots and evidence
├── Case-01-Shopping-Allegro/
│   ├── README.md
│   └── screenshots
├── Case-02-Login-Pinjaman/
│   ├── README.md
│   └── screenshots
├── Case-03-Parcel-Tracking/
│   ├── README.md
│   └── screenshots
├── Case-04-Netflix-Upgrade/
│   ├── README.md
│   └── screenshots
└── Case-05-Framer-Abuse/
    ├── README.md
    └── screenshots
    
