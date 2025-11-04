# Ability to use browser tools to get session secrets

Date: Sept 27, 2025<br/>
Classification: **Not an issue**<br/>
Source: `<verifying email they requested to share>`<br/>
Payment: $0<br/>

### Original Report

```
Hello,

Summary:
The system allows login without requiring a password or email, relying solely on a session cookie. This effectively means that possession of the __session cookie grants full account access, bypassing 2FA and other protections.

Steps to Reproduce:

 1. Open a browser and navigate to the login page.

 2. Install a browser extension such as Cookie Editor.

 3. Insert a valid __session cookie value into the browser.

 4. Refresh the page – you are logged in as the corresponding user.

 5. (Verification) In a second browser, log into an account normally. Extract the __session cookie via Cookie Editor and paste it into another browser → full account access is granted after refreshing the page.

Impact:

 • If an attacker obtains session cookies (e.g., via a stealer/malware), they can gain full access to the victim’s account.

 • This includes access to the control panel and a full account takeover.

 • Two-factor authentication and any other security mechanisms can be maybe bypassed.

 • Old session cookies remain valid after a new cookie is issued. If a user refreshes and receives a new __session cookie, the previous cookie is not invalidated and can still be used by an attacker to log in.  

Recommendation / Patch:


 • Do not allow cookie-only login.

 • Require proper authentication (email + password, and 2FA if enabled) even when a session cookie is present.

 • The token should be invalidated after a new one created.

Thanks!
If you need further information or assistance, please contact me.
```

This is how the internet works, clients need some form of token to authenticate requests.
