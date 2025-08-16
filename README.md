Phishing Email Analysis Lab
🔹 Objective

The purpose of this lab is to analyze a phishing email pretending to be from Chase Bank, identify technical indicators, and demonstrate how to trace the email headers and infrastructure behind the attack.

This lab shows step-by-step investigation of the email headers, IP addresses, authentication checks, and how to document findings for incident response.

🔹 Email Overview

From: alerts@chase.com (spoofed)

To: Bob Sanders <bob.sanders@corhalitech.com>

Subject: Your Bank Account has been blocked due to unusual activities

Reply-To: kellyellin426@proton.me

Return-Path: kellyellin426@proton.me

Date: May 01, 2024

🔹 Key Observations

Sender Spoofing

The email appears to come from alerts@chase.com.

However, the Return-Path and Reply-To reveal the real malicious actor: kellyellin426@proton.me.

Mail Server Used

Originating IP: 185.70.40.140

Host: mail-40140.protonmail.ch

Belongs to Proton Technologies AG (Switzerland) → legitimate provider often abused by threat actors for anonymity.

SPF, DKIM, DMARC Results

SPF: ✅ Pass (ProtonMail allowed)

DKIM: ❌ Timeout (key not validated)

DMARC: ✅ Pass (protonmail.com domain)

These checks passed because the attackers used ProtonMail’s real infrastructure, not because the email was genuine from Chase.

Phishing Indicators

Urgent subject line: “Your Bank Account has been blocked…”

Mismatch between From and Reply-To.

Financial brand impersonation (Chase).

Likely malicious links or instructions inside (payload not included in header excerpt).

🔹 Technical Analysis
WHOIS on IP 185.70.40.140
NetName:   protonmail-1  
Org:       Proton Technologies AG  
Country:   Switzerland  
Role:      Proton NOC  
Address:   Route de la Galaise 32, 1228 Plan-les-Ouates, Switzerland  


ASN: AS62371 PROTON Proton AG

Abuse contact: (hidden in sample, but usually abuse@protonmail.ch)

Mail Flow Trace

Message originated from ProtonMail server mail-40140.protonmail.ch (185.70.40.140)

Routed through Microsoft O365 filtering infrastructure (Exchange servers in the log).

Delivered to target’s inbox.

🔹 Attack Flow

Attacker registers free ProtonMail account (proton.me).

Crafts spoofed email using alerts@chase.com in the From field.

Sends phishing email through ProtonMail SMTP servers.

Recipient receives email appearing to be from Chase Bank.

Victim is lured into clicking a link or replying → credentials/financial theft.

🔹 Defensive Measures

Always check headers to spot mismatches.

Block suspicious Reply-To domains (proton.me in this case).

Train users to recognize urgency + finance + email spoofing as phishing red flags.

Deploy DMARC policies with reject/quarantine for financial institutions.

Report abuse to ProtonMail.

🔹 Conclusion

This lab demonstrated a phishing attempt where attackers used ProtonM<img width="1280" height="771" alt="Screenshot From 2025-08-16 10-15-00" src="https://github.com/user-attachments/assets/3c6f4c00-ee97-4a45-886d-c6cd373bbbc6" />
<img width="1280" height="771" alt="Screenshot From 2025-08-16 10-15-00" src="https://github.com/user-attachments/assets/8fb3ac3d-c74e-4238-94cb-f6fdc68829f9" />
ail servers to spoof Chase Bank. By analyzing the headers, IPs, and authentication checks, we uncovered the deception and documented the attack path.

📌 Skills Showcased:

Email header analysis

IP/WHOIS investigation

Understanding SPF, DKIM, DMARC

Phishing detection & reporting

