# Email change should invalidate sessions

Date: Aug 20, 2026<br/>
Classification: **Low**<br/>
Source: `Yaseen Zubair`<br/>
Payment: $50<br/>

### Original Report

```
Vulnerability: Failure to Invalidate Session on Email Address Change
Severity: Medium

Description:
The application does not invalidate active user sessions after an email address change. Changing an email address is a sensitive account operation because the email is commonly used for authentication, account recovery, and security notifications.

During testing, it was observed that when a user updates their email address, all existing sessions remain active and continue to grant full access to the account. This behavior indicates improper session management and allows previously authenticated sessions to persist even after a critical account identifier has been modified.

OWASP Reference:
A07:2025 - Authentication Failures

Steps to Reproduce:
 1. Log in to the same user account in two different browsers or devices.
 2. From the first browser, navigate to account settings.
 3. Change the email address associated with the account.
 4. From the second browser, refresh the page or perform any authenticated action.
 5. Observe that the session remains active without requiring re-authentication.
Impact:
 • An attacker who has access to a stolen or shared session can retain full account access even after the email address is changed.
 • Legitimate users are unable to fully secure their account by updating their email address.
 • Account recovery and security notifications may be redirected while unauthorized access persists.
 • This weakness can be chained with other issues to enable long-term unauthorized account access.
Recommendations:
 • Invalidate all active sessions immediately after an email address change.
 • Require users to re-authenticate after updating sensitive account information.
 • Prompt the user to confirm their password before allowing an email change.
 • Ensure session tokens are rotated or revoked when critical account attributes are modified.
References:
 • https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html
 • https://owasp.org/www-project-top-ten/Authentication_Failures
```

It was intended behavior, but we decided to change it. We agreed it would more likely match user expectations.

