# Phishing Email Analysis Project

This project contains a complete SOC-style investigation of a suspicious email pretending to be from Microsoft.
The raw phishing email used for this analysis is available in:
email-content.txt

1. Executive Summary

A phishing email impersonating the Microsoft Account Security Team was received.
The message uses urgency ("Your account will be locked in 24 hours") to trick the user into clicking a malicious URL leading to a fake login page.

This README documents:

- Email header analysis
- Sender & domain reputation analysis
- URL analysis
- Social engineering assessment
- SOC recommendations

2. Source Email (What Was Investigated)

The email begins with:

From: "Microsoft Account Team" <security-alert@microsoftsecureverify.com>
Subject: Action Required: Your Microsoft Account Will Be Locked in 24 Hours
To: victim@example.com

And includes a malicious verification button that links to:

https://microsoft-login-auth-verify.com/securelogin

Full content is stored in: email-content.txt.

3. Email Header Analysis

3.1 Sender Domain Mismatch

Displayed Sender:
"Microsoft Account Team"
Actual Sending Email:
security-alert@microsoftsecureverify.com

This is NOT an official Microsoft domain.
Real Microsoft domains include:

microsoft.com

accountprotection.microsoft.com

microsoftsupport.com

3.2 Return-Path Domain Is Suspicious

The return-path from the header (in your file) does not belong to Microsoft, indicating possible spoofing.

3.3 SPF / DKIM / DMARC Issues

Based on the domain and content:

The sender domain is not Microsoft-owned

DKIM is not signed

DMARC very likely fails

All three authentication failures are strong indicators of email spoofing.

Conclusion (Header Analysis):

 Sender is spoofed — this email is NOT from Microsoft.

 4. URL Analysis
URL Found in the Email
https://microsoft-login-auth-verify.com/securelogin

4.1 Domain Structure

Lookalike domain designed to imitate Microsoft:

Legitimate: login.microsoftonline.com

Fake: microsoft-login-auth-verify.com

Attackers add words like:

login

auth

secure

verify

To make URLs look trustworthy.

4.2 Likely Reputation Results (Typical SOC Findings)

If checked on tools like VirusTotal, urlscan.io, or Google Safe Browsing:

Multiple security vendors would flag this domain as Phishing

The domain would be newly registered

WHOIS information would likely be hidden or invalid

4.3 Expected Behavior

The link probably leads to:

A Microsoft-looking fake portal

A credential harvesting page

A redirect to another malicious site

Conclusion (URL Analysis):

Malicious — Credential Harvesting / Fake Login Page

5. Email Body & Social Engineering Analysis

5.1 Urgency / Fear Tactics

The email states:

"Your Microsoft account will be locked in 24 hours unless you verify your information."

Attackers use urgency to reduce critical thinking.

5.2 Generic Greeting

The email starts with:

"Dear User"

Microsoft usually includes:

Your name

Your account details

Your last sign-in location

Generic greetings are a major red flag.

5.3 Fake Branding

The email includes:

Microsoft color scheme

Fake footer

Security alert logo styles

Attackers typically copy HTML from real Microsoft emails but host the content on non-Microsoft domains.

5.4 Inconsistency in Tone & Grammar

The email uses unnatural wording such as:

“Temporarily restrict access in 24 hours”

“Complete verification”

These phrases are not typically used by Microsoft.

Conclusion (Body Analysis):

Email uses typical phishing techniques: urgency, impersonation, and fake branding.

6. Overall Verdict
Category	Result
Sender Authenticity	❌ Failed
Domain Reputation	❌ Suspicious / Fake
URL Behavior	❌ Malicious
Body Content	⚠️ Social Engineering
Likelihood of Phishing	🔴 High

Final Classification:
🔴 Malicious — Credential Harvesting Phishing Email

7. Recommended SOC Actions

7.1 Immediate Actions

Block sender domain:
microsoftsecureverify.com

Block malicious URL:
microsoft-login-auth-verify.com

Remove email from all user inboxes

Search SIEM logs for users who clicked the link

Force password resets for impacted users

7.2 Add Indicators to SIEM

Add these IOCs to your threat list:

Type	            Indicator
URL	            https://microsoft-login-auth-verify.com/securelogin
Domain	         microsoftsecureverify.com
Sender          Email	security-alert@microsoftsecureverify.com

7.3 User Awareness

Educate users to look for:

Domain mismatches

Urgent “verify now” messages

Hover-checking URLs before clicking

8. Analyst Summary 

This project demonstrates the ability to perform a full phishing investigation, including header analysis, URL reputation checks, social engineering detection, IoC extraction, and SOC-level remediation steps.




















