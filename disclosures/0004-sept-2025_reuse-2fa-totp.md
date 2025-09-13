# 30s 2FA codes are not invalidated after use

Date: Sept 2, 2025<br/>
Classification: **Low (best practices, minor issues)**<br/>
Source: `<asked not to be named>`<br/>
Payment: none<br/>

```
Hello,

Summary: The system allows the reuse of the same Google Authenticator (TOTP) code multiple times within or across login sessions, enabling an attacker to bypass the intended one-time nature of 2FA codes and gain unauthorized access.

Steps to Reproduce:

Enable 2FA (Google Authenticator) on your account.
 • Open Browser 1
   • Navigate to the login page.
   • Enter your email and password.
   • Proceed to the 2FA prompt (page waiting for the TOTP code).
 • Open Browser 2
   • In a separate browser (or private/incognito window), repeat the same steps:
   • Enter the same email and password.
   • Reach the 2FA prompt in this second session.
 • Generate TOTP Code
   • Open your Google Authenticator app.
   • Look up the current 6-digit code.
 • Enter TOTP Code in Browser 1
   • Type the current 6-digit code into Browser 1.
   • Submit and confirm successful login.
 • Quickly Switch to Browser 2
   • Enter the exact same code into Browser 2.
   • Submit the code.

Observe that the system accepts the reused code, allowing repeated logins.

Each TOTP code should be accepted only once and should be marked as used after a successful authentication attempt to prevent replay attacks.

Patch : Don't allow same otp check timestamp 

Thanks !
```

> This is a known issue and called a replay attack. 2FA adds extra security to your login credentials. If an attacker knew your login credentials and was able to watch your screen while you entered a 2FA code they could gain access to your account. Because of the difficulty to exploit and the complication & annoyances of invalidating 30s 2FA codes I do not plan to address this attack vector anytime soon.
