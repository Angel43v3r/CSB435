# Lab 7 - Validate Dumb Password Rules & Cookie Security Analysis

## Table Of Contents
1. [Overview](#overview)
2. [Part 1: Validate Dumb Password Rules](#part-1-validate-dumb-password-rules)
3. [Part 2: Cookie Security Analysis](#part-2-cookie-security-analysis)
4. [Submission](#submission)


## Overview
This multi-part assignment explores real-world password security practices and cookie security implementations. You'll investigate password policies on actual websites and analyze how cookies are used for session management.

## Part 1: Validate Dumb Password Rules

Visit https://dumbpasswordrules.com/ and look through the list of sites.

Our goal is to vet and improve the list by updating for changes, and finding new sites that belong here.

In order to prevent us from duplicates, we will use our slack channel to coordinate.

### Lab Instruction:
Pick ~5 sites that you can test, both that are on the Dumb Password Rules list and that are not on the list.

These can be sites you already have an account for or which you're willing to set up an account for.

Each time you prepare to test a site, post it in our slack channel so we don't duplicate.

https://app.slack.com/client/T03D19GLCBG/C07NWFLBDJ7

1. Attempt to change your password (if you already have an account) or create a new account
2. Test the password requirements to see if they match what's listed on the Dumb Password Rules site
3. Submit an MR/Issue to the Dumb Password Rules site if
- it no longer has dumb rules
- the dumb rules have changed
- it deserves to be on the list and wasn't yet

What would qualify for dumb password rules 1. Look for common anti-patterns: * Too-short maximum password length restrictions * Disallowing special characters * Requiring specific special characters * Preventing spaces in passwords * Forcing frequent password changes * Overly specific character requirements

If you've submitted 2 PRs you can move on from this lab section - that's plenty!

## Part 2: Cookie Security Analysis
Analyze how a real website uses cookies for authentication and session management.

Choose a website that:

- Requires login/authentication
- You have an account on (or can create one)
- Preferably a site you actually use

### Lab Instructions
1. Open an incognito/private browsing window (ensures no existing cookies)
2. Before logging in:
- Open browser DevTools (F12)
- Navigate to Application > Storage > Cookies (Chrome) or Storage > Cookies (Firefox)
- Load the site's main page (do NOT log in yet)
- Document all cookies present
3. After logging in:
- Log in to the site
- Check cookies again
- Document any new or changed cookies

### Cookie attributes to document
For each cookie, record at least the following:
- Cookie name
- When it was present (may be multiple)
    - before-login
    - after-login
    - after-logout
- Domain
- Path
- Expiration / Max-Age (or "Session" if it's a session cookie)
- Size in bytes (eyeball this, round to nearest 20 or so)
- HttpOnly flag (Yes/No)
- Secure flag (Yes/No)
- SameSite setting (None/Lax/Strict, or not set)
- Guess about what it's used for

### Example table format
Here's an example markdown table format

| Name       | Presence     | Domain      | Path | Expires  | Size | HttpOnly | Secure | SameSite | Purpose             |
| ---------- | --------     | --------    | ---- | -------  | ---- | -------- | ------ | -------- | ------------------- |
| session_id | after-login  | example.com | /    | Session  | 20   | Yes      | Yes    | Lax      | session management  |
| utm-01     | before-login | example.com | /    | 10 years | 80   | No       | Yes    | None     | analytics/tracking? |

## Submission

### Dumb Password Rules
- Which site(s) you tested
    - Were they on the list already or not?
    - Did they need updating?
1. Capital One 
    - Already in Dumb Password Rules
    - Yes it needed to be updated and removed in dumb password rule. The special character and spaces issue has been fixed.
2. GoDaddy
    - Already in Dumb Password Rules
    - Yes it needed to be updated and removed in dumb password rule. The special character issue has been fixed.
3. Gmail
    - Not in Dumb Password Rules
    - No it doesn't have any dumb password rules
4. X app
    - Not in Dumb Password Rules
    - No it doesn't have any dumb password rules
5. Instagram
    - Not in Dumb Password Rules
    - I couldn't test this one, it sent a malformed email to reset password.

- Links to any Pull Requests or issues you created
    - https://github.com/duffn/dumb-password-rules/issues/615
    - https://github.com/duffn/dumb-password-rules/issues/615

### Cookie Analysis
Which site(s) you analyzed
- Gmail

Cookie table
| Name              | Presence     | Domain             | Path            | Expires    | Size | HttpOnly | Secure | SameSite | Purpose             |
| ----------------- | --------     | ---------------    | --------------- | ---------- | ---- | -------- | ------ | -------- | ------------------- |
| _Host-GAPS        | before-login | accounts.google.com| /               | 2027-06-26 | 60   | Yes      | Yes    |          | Account Security & Sign-in Management |
| NID               | before-login | .google.com        | /               | 2026-11-21 | 211  | Yes      | Yes    | None     | Personalization & Logged-Out Ad Targeting |
| OTZ               | before-login | accounts.google.com| /               | 2026-06-21 | 33   |          | Yes    |          | Analytic & Security Tracking |
| _Securer-1PAPISID | after-login  | .google.com        | /               | 2027-06-26 | 51   |          | Yes    |          | Security and Marketing Cookie  |
| __Secure-1PSID    | after-login  | .google.com        | /               | 2027-06-26 | 167  | Yes      | Yes    |          | Primary Account Aunthentication and Profiling |
| __Secure-1PSIDCC  | after-login  | .google.com        | /               | 2027-05-22 | 90   | Yes      | Yes    |          | Security Verification and Anti-Fraud Cookie |
| __Secure-3PAPISID | after-login  | .google.com        | /               | 2027-06-26 | 51   |          | Yes    | None     | Authentication & Personalization Cookie |
| __Secure-3PSID    | after-login  | .google.com        | /               | 2027-06-26 | 167  | Yes      | Yes    | None     | Secure Authentication, Personalization, and  Ads |
| __Secure-3PSIDCC  | after-login  | .google.com        | /               | 2027-05-22 | 88   | Yes      | Yes    | None     | Security, Personalization, and  Ads |
| __Secure-OSID     | after-login  | mail.google.com    | /               | 2027-06-26 | 166  | Yes      | Yes    | None     | Sign-in Management & Authentication |
| APISID            | after-login  | .google.com        | /               | 2027-06-26 | 40   |          |        |          | Identification, Personalization, and  Ads |
| COMPASS           | after-login  | mail.google.com    | /mail/u/0       | 2026-06-01 | 621  | Yes      | Yes    | None     | Analytics, Personalization, and  Ads |
| GAUSR             | after-login  | mail.google.com    | /mail/mu/mp/954 | 2027-06-26 | 28   |          |        |          | Analytics & Personalization | 
| GM_IMP            | after-login  | mail.google.com    | /mail/u/0/s/    | 2027-05-25 | 6    |          |        |          | Analytics, Ads, Performance | 
| GM_RUNNING        | after-login  | mail.google.com    | /mail/u/0/s/    | 2027-05-25 | 11   |          |        |          | Session Tracking & Analytics | 
| GMAIL_AT          | after-login  | mail.google.com    | /mail/mu/mp/954 | Session    | 42   |          | Yes    |          | Authentication & Maintain Sign-in State  | 
| GX                | after-login  | mail.google.com    | /mail           | 2027-06-26 | 7    | Yes      | Yes    |          | Session Tracking  | 
| HSID              | after-login  | .google.com        | /               | 2027-06-26 | 21   | Yes      |        |          | Authentication & Session Integrity |
| OSID              | after-login  | mail.google.com    | /               | 2027-06-26 | 157  | Yes      | Yes    |          | Authentication & Session Management |
| SAPISID           | after-login  | .google.com        | /               | 2027-06-26 | 41   |          | Yes    |          | Authentication, Identification, Personalization & Ads  |
| SDP_PROMO_SHOWN   | after-login  | mail.google.com    | /mail/mu        | 2026-05-29 | 19   |          |        |          | Promotional Message |
| SID               | after-login  | .google.com        | /               | 2027-06-26 | 156  |          |        |          | Authentication & Session Management  | 
| SIDCC             | after-login  | .google.com        | /               | 2027-05-22 | 79   |          |        |          | Security and Fraud Prevention  | 
| SSID              | after-login  | .google.com        | /               | 2027-06-26 | 21   | Yes      | Yes    |          | Authentication & Session Management  | 
| WML               | after-login  | mail.google.com    | /mail           | 2027-06-26 | 46   |          | Yes    |          | Analytic & Tracking |

Your observations about the cookies:
Which cookies appear to be for authentication/session management?

- __Secure-1PSID, __Secure-3PAPISID, __Secure-3PSID, __Secure-OSID, GM_RUNNING, GMAIL_AT, GX, HSID, OSID, SAPISID, SID, and SSID

Are the authentication cookies properly secured (HttpOnly, Secure, SameSite)?

- Yes almost all except APISID, GAUSR, GM_IMP, GM_RUNNING, SDP_PROMO_SHOWN, SID, and SIDCC

Are there any cookies that seem unnecessary or overly permissive?

- Yeah there are some that does Ad targetting, promo and personalization which is overly permissive and unnecessary. For example SDP_PROMO_SHOWN is a promotional message which is unneccessary. 

Another is NID which is also just for personalization and Ad targetting. 

Do any cookies have concerning lifetimes (too long or too short)?

- I think most are appropriate but some are too long like some are like expires in 1 year.