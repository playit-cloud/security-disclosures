# Absence of Anti-CSRF Tokens on website

Date: Sept 2, 2025<br/>
Classification: **Medium (CSRF with impact, reflected XSS, limited data exposure)**<br/>
Source: [https://aboutme.hammess404.win](https://aboutme.hammess404.win), [https://github.com/lkspodmol](https://github.com/lkspodmol)<br/>
Payment: $200<br/>
Status: resolved<br/>

### Original Report
```
Hey there! I was a little bit bored and I was researching the web for some common vulnerabilities and found this.

Absence of Anti-CSRF Tokens

If playit.gg/login does not have implemented Anti-CSRF tokens, then an attacker could craft a malicious webpage that issues forged POST requests to the login-protected endpoints while a victim’s browser has an active session, and without a validated CSRF token the server will execute these requests with the victim’s credentials, potentially allowing state-changing actions to be performed without user consent.  

https://cwe.mitre.org/data/definitions/352.html

Have a nice day!
```

> Initially dimissed report due to CORS headers protecting against cross site requests but was unsure so planned to investigate the issue further. On Sept 9th I found an issue and followed up.

```
I've been doing some more reading. Because we still have some users with .playit.gg sub domains assigned to their account, those users could create phishing websites that would be able to POST using secure sessions. I can confirm, CSRF is an issue. I'll be working to resolve this week. Thank you for following up with me.
```

> Sept 17th I did testing to confirm the issue and pushed a fix to our website.
