# Unused password reset code is not invalidated if user changes their email

Date: Sept 2, 2025<br/>
Classification: **Low (best practices, minor issues)**<br/>
Source: `<asked not to be named>`<br/>
Payment: $50<br/>

### Original Report
```
Hi,

Description:

When a user changes their password from the account settings, previously generated password reset tokens remain valid. This allows an attacker who has intercepted or obtained an old reset token to still reset the password, even after the legitimate user has changed their password.

Steps to Reproduce:

 1. Generate a password reset token by initiating a "Forgot Password" request.
 2. Do not use the token immediately.
 3. Log in with the account and change the password from the Settings page.
 4. Use the old reset link generated before the password change.
 5. Observe that the old reset token is still valid, allowing password reset.

Impact:

 • This breaks the expectation of session/token invalidation upon sensitive account changes.
 • An attacker who obtained a reset token earlier can still compromise the account after the user has updated their password.
 • This can lead to full account takeover.

Thanks !
```

> I agree, we should invalidate our password reset code if the user changes their email address. The code already expires based on timestamp but I think a user could expect the reset code to be invalidated and is a safer behaviour.
