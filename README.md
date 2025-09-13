# Security Disclosures

> [!CAUTION]
> If you have found a security vulnerability with a playit service or product **DO NOT SHARE HERE**, email details to **security@playit.gg**.


# Playit.gg Bug Bounty Policy

## 🎯 Scope

**In scope**
- `playit.gg` and `api.playit.gg` (our main web app and APIs)
- Non deprecated releases of the [official playit program](https://github.com/playit-cloud/playit-agent)
- Authentication, login, and account management
- Payment and billing systems
- Session handling, cookies, and data security

**Out of scope**
- Denial of Service (DoS) or brute force attacks
- Spam, phishing, or social engineering against staff or users
- Issues in third-party services outside of our control
- Low-impact issues such as:
  - Missing or non-critical HTTP headers
  - Clickjacking on non-sensitive pages
  - Account enumeration via generic error messages

---

## ⏸ Audit Freeze Periods

From time to time, playit may engage in **paid third-party security audits**. During these periods, we temporarily **pause the bug bounty program** and do not accept or pay for external security disclosures.

**Rationale:**  
- External audits often involve deep testing that would overlap with community reports.  
- Running both simultaneously creates duplicated effort and wasted resources.  
- Pausing ensures we can focus on fixing findings quickly without split attention.  

When a freeze is in effect, we will post a notice on our [Github Page](https://github.com/playit-cloud/security-disclosures) and provide dates. Reports submitted during a freeze will not be eligible for bounty consideration but may be re-evaluated if resubmitted after the freeze ends.

---

## 💰 Rewards

> [!IMPORTANT]
> We **do not** guarantee payment or rewards for disclosures. We are small company and if we do not have the available funds to pay, we will not be able to pay. Please see [Disclosure History](DISCLOSURE_HISTORY.md) to evaluate how we've done rewards in the past. If we're not paying out rewards consistently per these guidelines, our shameful acts will be shared there.

We try to pay bounties based on severity and impact. Reports are scored using CVSS guidelines, with adjustments for real-world risk to playit and our users.

- **Critical (RCE, full account takeover):** $1,000 – $2,000
- **High (privilege escalation, stored XSS on auth/billing, significant data exposure):** $500 – $1,000
- **Medium (CSRF with impact, reflected XSS, limited data exposure):** $200 – $500
- **Low (best practices, minor issues):** $50 – $100 or recognition only

**Limits**
- Max payout per report: **$2,000**
- Monthly program cap: **$5,000**

---

## 📜 Rules

- **Safe Harbor:** We will not pursue legal action for good-faith testing and reporting.
- Never disrupt service or access data that isn't yours.
- Do not publicly disclose before we've had time to fix the issue (30–90 days).
- Duplicate reports are closed as already known (first valid report earns the bounty).
- One payout per unique issue.
- Unless adequately justified, all security disclosures will be shared publicly when resolved with any rewards or payments detailed. You can choose to have public recognition.
- To receive payment, you may be required to complete tax forms such as a W-9 or W-8BEN.

---

## 📩 Reporting

Send reports to **security@playit.gg** with:
- A clear description of the vulnerability
- Steps to reproduce (proof of concept if possible)
- Suggested remediation (if available)

We commit to:
- Acknowledging your report within 5 business days
- Weekly updates until resolution
- Payment within **30 days** of validation

---

## 🏆 Recognition

For transparency, we maintain a [Disclosure History](DISCLOSURE_HISTORY.md) page. This shows:
- Past reports we've received and either dismissed or resolved
- The rewards we paid
- How we evaluated each disclosure

We encourage you to review it to understand how playit rewards security research in practice. Reports provided before this project may be lacking details or missing entirely.
