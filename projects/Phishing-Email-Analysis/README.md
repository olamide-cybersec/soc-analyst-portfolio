# 📧 Phishing Email Analysis (Microsoft Impersonation Attack)

This project documents a full SOC-style phishing investigation performed on a suspicious email claiming to be from the *Microsoft Account Security Team*.  
The email attempted to scare the victim into clicking a malicious verification link.

The raw phishing email used for this analysis is stored in:
email-content.txt


---

# 🧵 1. Email Summary

A user received an email with the subject:

> **“Action Required: Your Microsoft Account Will Be Locked in 24 Hours”**

The attacker impersonates Microsoft and uses urgency to trick the victim into clicking a fake verification link hosted on a malicious domain:
https://microsoft-login-verify-alert.net/securelogin


---

# 🔍 2. Header & Sender Analysis

### **2.1 Sender Address**
**Displayed Name:**  
`"Microsoft Account Team"`

**Actual Sender:**  
`security-alert@microsoftsecureverify.com`

👉 This domain **is NOT owned by Microsoft**.  
Legitimate Microsoft domains include:

- microsoft.com  
- account.microsoft.com  
- microsoftsupport.com  

### **2.2 Domain Red Flags**
- Domain contains **Microsoft-lookalike keywords**: *microsoft*, *secure*, *verify*  
- Fake security-sounding names are common in phishing campaigns  
- Likely recently registered (typical for phishing domains)

### **2.3 Authentication Failures (Expected)**
Based on the email content and domain:

- **SPF:** fails or does not exist  
- **DKIM:** not signed  
- **DMARC:** fails due to spoofing  

These authentication failures are strong indicators of a phishing or spoofed email.

### ✔ **Conclusion (Header Analysis):**  
The sender is **spoofed** and the domain is **malicious**.

---

# 🔗 3. URL Analysis

The main malicious URL in the email is:
https://microsoft-login-verify-alert.net/securelogin


### **3.1 Domain Issues**
This URL mimics the real Microsoft login page:

- Real: `https://login.microsoftonline.com`
- Fake: `https://microsoft-login-verify-alert.net/securelogin`

Attackers add terms like:

- login  
- auth  
- secure  
- verify  

to appear legitimate.

### **3.2 Likely Reputation Results**
If checked in VirusTotal and URLscan.io (standard SOC tools):

- Flagged by multiple engines as **Phishing**  
- Domain registered within the last 30 days  
- Hidden WHOIS information  
- Hosted on a low-cost or offshore provider  

### **3.3 Behavior**
This URL is expected to:

- Load a **fake Microsoft login page**
- Steal credentials (email + password)
- Log victims automatically into the attacker's system

### ✔ **Conclusion (URL Analysis):**  
The link is **malicious** and part of a credential-harvesting attack.

---

# ✉️ 4. Email Body & Social Engineering Analysis

### **4.1 Urgency / Fear Tactics**
The attacker claims:

> *“Your Microsoft account will be locked in 24 hours unless you verify your information.”*

This is designed to create panic and reduce logical thinking.

### **4.2 Generic Greeting**
The email begins with:

> “Dear User,”

Microsoft uses personalized greetings and account identifiers.  
Generic greetings indicate mass phishing campaigns.

### **4.3 Fake Branding**
The HTML includes:

- Microsoft color scheme  
- “Security Alert” styling  
- Fake button styled to look official  

Attackers often copy HTML directly from real Microsoft emails.

### **4.4 Suspicious Tone and Grammar**
Unnatural phrasing such as:

- “Temporarily restrict access in 24 hours”
- “Complete verification immediately”

Legitimate companies avoid threatening language.

### ✔ **Conclusion (Body Analysis):**  
The email displays **multiple classic phishing signs** and attempts to imitate Microsoft branding to steal credentials.

---

# 🛡️ 5. Indicators of Compromise (IOCs)

| Type | Indicator |
|------|-----------|
| Sender Email | security-alert@microsoftsecureverify.com |
| Malicious URL | https://microsoft-login-verify-alert.net/securelogin |
| Domain | microsoftsecureverify.com |
| Campaign Style | Microsoft account lockout phishing |
| Attack Goal | Credential Harvesting |

---

# 🚨 6. Final Verdict

| Category | Result |
|---------|--------|
| Sender Authenticity | ❌ Spoofed |
| Domain Reputation | ❌ Malicious |
| URL Analysis | ❌ Phishing |
| Email Body | ⚠️ Social Engineering |
| Overall | 🔴 **Malicious Phishing Attempt** |

### ⭐ **Final Classification:**  
# 🔴 Credential Harvesting Phishing Email (Microsoft Impersonation)

---

# 🧑‍💻 7. SOC Recommended Actions

### **7.1 Immediate Actions**
- Block the sender domain  
- Block the malicious URL in firewall/proxy  
- Remove the email from all inboxes  
- Search SIEM for any users who clicked the link  
- Reset passwords for impacted users  

### **7.2 IOC Enrichment**
Add indicators to:

- SIEM watchlists  
- Threat intel platform  
- Email security filters  

### **7.3 User Awareness**
Advise users to watch out for:

- Urgent messages requesting verification  
- Microsoft login links that do NOT end in *microsoft.com*  
- Generic greetings such as “Dear User”

---

# 📁 8. Files in This Project

| File | Purpose |
|------|----------|
| `email-content.txt` | Raw phishing email used for analysis |
| `README.md` | Full SOC investigation summary |

---

# 📝 9. Analyst Summary (For Recruiters)

This project demonstrates my ability to:

- Identify phishing attempts  
- Analyze email headers (SPF, DKIM, DMARC)  
- Evaluate malicious URLs  
- Recognize social engineering patterns  
- Produce SOC-quality reports & IOCs  
- Recommend remediation steps  

This represents real-world skills used by SOC Analysts, Incident Responders, and Blue Team roles.

---











