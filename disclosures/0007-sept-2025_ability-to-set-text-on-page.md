# Ability to set text in form element on page via URL

Date: Sept 24, 2025<br/>
Classification: **Low (best practices, minor issues):**<br/>
Source: `<asked not to be named>`<br/>
Payment: $0<br/>
Status: May address in the future<br/>

### Original Report
```
Hi,

Description : The /login/reset-password/:token endpoint improperly renders or allows crafted strings in the :token path parameter. This allows malicious actors to inject social engineering or phishing messages into URLs.

Steps to Reproduce

Go to: https://playit.gg/login/reset-password/THIS%20IS%20SECRET%20MESSAGE%20PLEASE%20VISIT%20ON%20WWW.HACK.COM%20AND%20DO%20LOGIN

Observe that the path is accepted and displayed without error.

A user may misinterpret this as a legitimate password reset request, especially if the attacker shortens the link or embeds it.

Potential Impact

Phishing risk: Attackers can craft links that appear legitimate.

Reputation risk: Your domain could be misused to spread malicious content.

User compromise: Could lead to credential theft or malware installation if users follow spoofed instructions.

Reference : https://owasp.org/www-community/attacks/Content_Spoofing

Thanks !
```

> I agree, we should not allow an attacker to render text to a page by tricking a user to click a link. However, I consider this very low risk and am not worried. When these pages get replaced and upgraded I will try to avoid this from being possible.

## Other

This reporter is no longer eligible for future monetary rewards in our security disclosure program. They have been informed of this decision.

This action follows an instance where vulnerabilities were publicly advertised before our review and remediation process could be completed, as well as disagreements regarding reward eligibility and amounts.

Disclosures from any researcher, including this individual, will continue to be accepted, reviewed, and, when appropriate, publicly recognized, even if no monetary reward is offered.
