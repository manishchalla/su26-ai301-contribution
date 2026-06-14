# AI301 Contribution README
**Student:** Manish Challa  
**GitHub:** [@manishchalla](https://github.com/manishchalla)  
**Course:** AI301 — AI Open Source Capstone, Summer 2026  
**Status:** Phase II Complete

---

## Contribution #1

**Issue:** [furpocalypse/APIS #53 — Clean up CSP](https://github.com/furpocalypse/APIS/issues/53)

---

## Phase I — Issue Selection

### Why I Chose This Issue
The APIS project has Content Security Policy (CSP) violations being logged 
in the developer console. The fix involves migrating from a third-party `csp` 
module to Django's built-in CSP functionality, adding missing domains and 
nonces, and cleaning up inline scripts and styles in templates. I chose this 
issue because it is a well-scoped Python/Django bug with a clear 4-step task 
list, tagged `good first issue` with `status:ready` confirmed by the 
maintainer. It aligns with my Python and web development skills and has a 
clear definition of done.

### Issue Summary
The APIS Django project currently uses a third-party `csp` module that is 
producing CSP violations in the developer console. These violations come from 
PayPal scripts on unexpected domains, inline script and style tags, and style 
attributes baked into templates. None of this breaks functionality currently 
since it runs in report-only mode, but it needs to be cleaned up by migrating 
to Django's built-in CSP support and properly configuring nonces and allowed 
domains.

### Links
- **Issue:** https://github.com/furpocalypse/APIS/issues/53  
- **My Fork:** https://github.com/manishchalla/APIS  

---

## Phase II — Reproduce & Plan

### Understanding the Issue

**Problem Description:**  
The APIS project uses the third-party `django-csp~=4.0` package for Content 
Security Policy management. The browser console logs multiple CSP violations 
because several external domains are missing from the allowlist (Sentry CDN, 
Google Fonts), inline scripts in templates lack nonces, and inline `style=` 
attributes exist in templates. Django 6.0 has built-in CSP support making 
the third-party package redundant. The settings.py already partially uses 
Django 6.0's CSP format (`CONTENT_SECURITY_POLICY_REPORT_ONLY`) suggesting 
a migration was started but never completed.

**Expected Behavior:**  
No CSP violations in the browser developer console. All scripts, styles, 
and fonts load correctly with proper nonces or allowlisted domains.

**Current Behavior:**  
The following CSP violations appear in the browser console on 
`http://localhost:8000/registration/`:
- `browser.sentry-cdn.com` blocked — not in `script-src` allowlist
- Inline scripts blocked — need nonces added to templates
- `fonts.googleapis.com` blocked — not in `style-src` allowlist
- Inline `style=` attributes blocked in multiple templates

**Affected Components:**  
- `fm_eventmanager/settings.py` — CSP configuration and allowlists
- `pyproject.toml` — dependency list (`django-csp~=4.0`)
- `templates/allauth/elements/img.html` — inline style attribute
- `templates/admin/registration/order/change_form.html` — inline styles

---

### Reproduction Process

**Environment Setup:**  
Used Docker Compose on WSL2 (Windows 11). Setup was straightforward 
following the README instructions:
```bash
git clone https://github.com/manishchalla/APIS.git
cd APIS
cp database.env.example database.env
docker compose up -d
docker compose exec app /app/manage.py bootstrap_admin
```
Stack was fully running within ~3 minutes after the initial build 
(~172 seconds for first build). No setup issues encountered.

**Working Branch:**  
https://github.com/manishchalla/APIS/tree/fix-issue-53-clean-up-csp

**Steps to Reproduce:**  
1. Clone the repo and run `docker compose up -d`
2. Run `docker compose exec app /app/manage.py bootstrap_admin`
3. Open `http://localhost:8000/registration/` in your browser
4. Press **F12** to open Developer Tools and click the **Console** tab
5. Observe the following CSP violation errors logged in the console:
   - `Loading the script 'https://browser.sentry-cdn.com/...' 
     violates CSP directive script-src`
   - `Executing inline script violates CSP directive script-src`
   - `Loading the stylesheet 'https://fonts.googleapis.com/...' 
     violates CSP directive style-src`

**Reproduction Evidence:**  
- Branch: https://github.com/manishchalla/APIS/tree/fix-issue-53-clean-up-csp
- CSP violations confirmed in browser console on 
  `http://localhost:8000/registration/`
- Violations are in report-only mode so nothing is broken but 
  violations are clearly logged
- Found inline styles in:
  - `templates/allauth/elements/img.html` line 2
  - `templates/admin/registration/order/change_form.html` lines 40, 55, 66

---

### Solution Approach

**Analysis:**  
The root cause is threefold:
1. `django-csp~=4.0` is still listed as a dependency but `settings.py` 
   already uses Django 6.0's built-in `CONTENT_SECURITY_POLICY_REPORT_ONLY` 
   format — indicating a partial migration that was never completed
2. The `script-src` allowlist is missing `https://browser.sentry-cdn.com`
3. The `style-src` allowlist is missing `https://fonts.googleapis.com`
4. Templates have inline `<script>` tags and `style=` attributes that 
   need nonces or CSS class replacements

**Proposed Solution:**  
Two possible approaches — awaiting maintainer confirmation on which to use:

- **Option A (Quick fix):** Keep `django-csp`, add missing domains to 
  allowlist, add nonces to inline scripts using `{% csp_nonce %}`
- **Option B (Full migration):** Remove `django-csp` entirely, complete 
  the migration to Django 6.0's built-in CSP, add missing domains and nonces

**Implementation Plan (UMPIRE):**

**Understand:**  
CSP violations occur because the allowlist is incomplete and inline 
scripts/styles in templates lack nonces. The project is mid-migration 
between `django-csp` and Django 6.0's built-in CSP.

**Match:**  
Django 6.0 docs show `CONTENT_SECURITY_POLICY` dict replaces `django-csp`. 
The existing `CONTENT_SECURITY_POLICY_REPORT_ONLY` dict in `settings.py` 
already uses this exact format — just needs the old package removed and 
missing domains added.

**Plan:**  
1. Remove `django-csp~=4.0` from `pyproject.toml`
2. Remove `"csp"` from `INSTALLED_APPS` in `settings.py`
3. Remove `"csp.middleware.CSPMiddleware"` from `MIDDLEWARE` in `settings.py`
4. Add `https://browser.sentry-cdn.com` to `script-src` in `settings.py`
5. Add `https://fonts.googleapis.com` to `style-src` in `settings.py`
6. Add nonces to inline `<script>` tags in templates
7. Replace inline `style=` attributes in templates with CSS classes

**Implement:**  
https://github.com/manishchalla/APIS/tree/fix-issue-53-clean-up-csp  
*(code changes coming in Phase III)*

**Review:**  
Will check `CONTRIBUTING.md` and follow the project's commit message 
conventions before opening PR. Will run `make test-django` to confirm 
no regressions.

**Evaluate:**  
After the fix, opening `http://localhost:8000/registration/` in the 
browser console should show zero CSP violations. Will run 
`make test-django` to confirm all 450+ existing tests still pass.

---

## Phase III — Testing & Implementation
*(Coming in Week 3)*

### Testing Strategy
**Unit Tests:**  
- Test case 1: [Description]  
- Test case 2: [Description]  

**Manual Testing:**  
[What you tested manually and results]

### Implementation Notes
**Week 2 Progress:**  
[What you built, challenges faced, decisions made]

**Code Changes:**  
- Files modified: [List]  
- Key commits: [Links]  
- Approach decisions: [Why you chose certain approaches]  

---

## Phase IV — Pull Request
*(Coming in Week 4)*

**PR Link:** [GitHub PR URL when submitted]  

**PR Description:**  
[Draft or final PR description]

**Maintainer Feedback:**  
- [Date]: [Summary of feedback received]  
- [Date]: [How you addressed it]  

---

## Learnings & Reflections
*(To be completed at end of program)*

**Technical Skills Gained:**  
[What you learned technically]

**Challenges Overcome:**  
[What was hard and how you solved it]

**What I'd Do Differently Next Time:**  
[Reflection on your process]
