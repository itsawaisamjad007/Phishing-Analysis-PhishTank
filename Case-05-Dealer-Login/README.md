# Phishing Analysis - PhishTank (5 Cases)

## Project Objective
I collected 5 different phishing URLs from PhishTank, analyzed them using VirusTotal, URLScan.io and Whois Lookup, and compared their techniques.

## Tools Used
- PhishTank - To collect live phishing URLs
- VirusTotal - To check URL detection
- URLScan.io - To view page safely without opening it
- Whois Lookup - To check domain creation date

## Comparison Table

| Case | Type | Domain | VirusTotal Score | Verdict |
| --- | --- | --- | --- | --- |
| Case 01 | Shopping / Allegro | allegrolokalnie.letnie-okazje491831.shop | 4/93 | CONFIRMED PHISHING |
| Case 02 | Loan / Pinjaman | ktadbs-pinjaman.blogspot.com.br | - | - |
| Case 03 | Parcel / Suivi | sskkbpk.pro | - | - |
| Case 04 | Airline / Annulation | annulation-airial.com | - | - |
| Case 05 | Dealer / Login | dealerops3.com | - | - |

## Key Findings
1. All used cheap TLDs: .shop, .pro, .com.br
2. All abused a trusted brand name
3. All used redirects to hide the real destination

## Indicators of Compromise (IoCs)
All IoCs are listed in `IoCs.txt`.

## Analyst
Awais - SOC Level 1 Aspirant