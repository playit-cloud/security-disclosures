# CSRF with plain/text request

Date: September 18, 2026<br/>
Classification: **Medium**<br/>
Source: `Gabriel`<br/>
Payment: $300<br/>

### Original Report

```
CSRF on state-changing API endpoints → account takeover (HIGH, CVSS 8.1, CWE-352)
--------------------------------------------------------------------------------

Description
  The web app authenticates to api.playit.gg with the session cookie `__Secure-WebAuth`,
  which is issued as `SameSite=None`. State-changing endpoints have no CSRF token, do not
  validate `Origin`/`Referer`, and accept non-JSON bodies (`text/plain`,
  `application/x-www-form-urlencoded`). Because `text/plain` is a CORS-safelisted content
  type, a cross-origin `fetch(..., {credentials:"include"})` is delivered with the victim's
  cookie and no preflight, so your strict CORS allowlist does not stop it. All three CSRF
  defenses (SameSite, Origin check, Content-Type enforcement) are absent.

Observed cookie:
  set-cookie: __Secure-WebAuth=...; HttpOnly; SameSite=None; Secure; Path=/; Max-Age=604800

Steps to reproduce
  1. Log in and confirm `__Secure-WebAuth` is `SameSite=None`.
  2. From an unrelated origin, send:
       POST https://api.playit.gg/login/email/change
       Content-Type: text/plain
       Origin: https://evil.example
       (credentials: include)
       Body: {"new_email":"attacker-controlled@example.com"}
     Response: 200 {"status":"success","data":"EmailChanged"} and the session is invalidated.
  3. Sign in with the new email + the original password → succeeds; the old email now returns
     IncorrectCredentials. The forged request changed the account's login identifier.
  4. The attacker (who controls the new inbox) completes takeover via the normal password-reset
     flow (`/login/reset/send` → `/login/reset/password`).
  The same primitive also renames/deletes firewalls, tunnels and agents, e.g.
       POST /firewalls/rename  Content-Type: text/plain  Origin: https://evil.example
       Body: {"firewall_id":"<id>","name":"CSRF-RENAMED"}   → 200, name changes.

Scope of validation (stated honestly)
  - Cross-origin acceptance of `text/plain`/form bodies with an arbitrary `Origin`: confirmed (HTTP 200).
  - Firewall rename via CSRF: confirmed live.
  - Immediate email change + login with new email: confirmed on an UNVERIFIED-email account.
  - On a VERIFIED-email account, `/login/email/change` returns `VerifyCodeSent` (new-email
    verification required), so single-request takeover is limited to unverified accounts;
    the resource rename/delete CSRF impact applies to all accounts.
  - The final password-reset-to-login hop was not executed end-to-end (it needs an
    attacker-controlled inbox); it is your standard documented reset flow.

Remediation
  - Set the session cookie to `SameSite=Lax` (or `Strict`), not `None`.
  - Enforce `Content-Type: application/json` on state-changing endpoints; reject `text/plain`
    and form-encoded bodies (e.g. 415).
  - Validate `Origin`/`Sec-Fetch-Site` against an exact `https://playit.gg` allowlist.
  - Add a per-session anti-CSRF token (or a custom header that forces a preflight) as
    defense-in-depth.
  - Require the current password or a one-time code for email change and other high-risk
    account changes.
```

Real issue. Fixed.

We were not aware that text/plain qualifies as a CORS simple request and can therefore be sent cross-origin without a preflight request. Because our API accepted these requests, a malicious website could blindly send authenticated POST requests on behalf of a logged-in user. The malicious website would not be able to read the API response due to CORS, but that does not prevent the request itself from being processed.

This allowed CSRF against state-changing API endpoints, including operations such as modifying firewalls, tunnels, and agents when the attack was targeted and the attacker had knowledge of resource IDs assigned to the account.

The reported account takeover impact was more limited. For accounts with a verified email address, changing the account email requires confirmation before the change is applied. However, as demonstrated in the report, accounts without a verified email address were able to have their email changed directly.

We have fixed the underlying issue so cross-origin simple requests can no longer be used to perform authenticated state-changing actions.
