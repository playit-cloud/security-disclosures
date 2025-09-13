# Login redirect has XSS vulnerability

Date: Sept 1, 2025<br/>
Classification: **Medium / High**<br/>
Source: `ashishpathakall@gmail.com`, [ashishpathaksec.blogspot.com](https://ashishpathaksec.blogspot.com)<br/>
Payment: $600<br/>
Status: resolved<br/>

### Original Report
```
Vulnerability : Cross Site Scripting 

Severity : Critical 
Summary : The login endpoint accepts a redirect parameter and executes it after successful authentication without proper validation. Passing a javascript: URL scheme leads to execution of attacker-controlled JavaScript in the context of playit.gg immediately after login, giving code access to the authenticated user’s session and page DOM.
Steps to Reproduce

Navigate to : https://playit.gg/login?redirect=javascript:alert(0);

Sign in with any valid account.

After successful login, an alert(0) pops — demonstrating script execution.
Thanks !
```

> This is a real issue and embarrassing issue, a quick but insufficient patch was made.

### Follow up report after first patch
```
Hi,

Description: The login endpoint of playit.gg is vulnerable to an open redirect due to improper validation of the redirect parameter. An attacker can supply an arbitrary external URL, and after login, the user is redirected to that attacker-controlled domain.

Proof of Concept (PoC):

 1. Navigate to:
https://playit.gg/login?redirect=http://google.com

 2. After login, the application redirects the user to http://google.com

Impact:

 • Phishing & Social Engineering: Attackers can trick users into logging in via the legitimate playit.gg domain but then redirect them to a malicious website.

 • Credential Theft: Users may unknowingly provide their credentials or sensitive data to attacker-controlled sites.

 • Reputation Damage: Trust in the playit.gg brand could be harmed if users are exploited through malicious redirects.

Reference : https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/11-Client_Side_Testing/04-Testing_for_Client_Side_URL_Redirect

Thanks !
```

> After initial patch, same researcher soon after made another report. Issue was patched again, hopefully this time for good. Researcher wanted an additional payment / reward. I decided not to provide an additional payment / reward.
