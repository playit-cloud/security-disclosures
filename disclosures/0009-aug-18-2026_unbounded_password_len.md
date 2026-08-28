# Unbounded password length

Date: Aug 18, 2026<br/>
Classification: **Low**<br/>
Source: `<verifying email they requested to share>`<br/>
Payment: $50<br/>

### Original Report

```
Hello there, 
We have found some serious vulnerabilities on your website one of which is below and would like to get more to your attention at your convenience. 

Vulnerability 1:
Target: https://playit.gg
Severity: Medium (Denial-of-Service)
Vulnerability Type: Unrestricted password length allows resource exhaustion

Description:
The registration form on https://playit.gg/login/create does not enforce a maximum length restriction for passwords. This allows users to submit arbitrarily long password strings. Processing these overly large inputs can consume excessive server resources, particularly during password hashing operations. As a result, this behavior can be exploited to perform a Denial-of-Service (DoS) attack.

Impact:
The absence of a password length limit exposes the server to potential abuse. An attacker could script multiple concurrent registration attempts with extremely long passwords, consuming server resources (especially CPU, during password hashing), potentially degrading performance or taking the service offline.

Proof of Concept (PoC):
A PoC demonstrating this issue is attached to this report. To summarize:
1. Navigate to the registration page at https://playit.gg/login/create.
2. Attempt to create an account using a password with excessive length (e.g., the text file attached).
3. Observe that the server accepts the input without validation errors or length restrictions.

Recommendation:
Implement a server-side password length constraint to limit the maximum password length to a reasonable value, such as 64 or 72 characters. This aligns with best practices and prevents abuse while allowing users sufficient password complexity.

References (Best Practices):
• OWASP Password Storage Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
• NIST Guidelines (SP 800-63B): Passwords should allow at least 64 characters but should also impose upper bounds to prevent DoS vectors.

If you have any questions or need further clarification, I would be happy to assist.

Thank you for your attention to this matter. I look forward to your response.
Best Regards,
<redacted, confirming if wished to be named>
```

Set a limit on password length.
