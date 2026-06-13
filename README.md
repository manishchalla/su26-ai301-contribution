# AI301 Contribution README
**Student:** Manish Challa  
**GitHub:** [@manishchalla](https://github.com/manishchalla)  
**Course:** AI301 — AI Open Source Capstone, Summer 2026  
**Status:** Phase I Complete

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
*(Coming in Week 2)*

### Understanding the Issue
**Problem Description:**  
[In your own words, what's broken or missing?]

**Expected Behavior:**  
[What should happen?]

**Current Behavior:**  
[What actually happens?]

**Affected Components:**  
[Which parts of the codebase are involved?]

### Reproduction Process
**Environment Setup:**  
[Notes on setting up your local development environment]

**Steps to Reproduce:**  
1. [Step 1]  
2. [Step 2]  
3. [Observed result]

**Reproduction Evidence:**  
- Commit showing reproduction: [Link to commit in your fork]  
- Screenshots/logs: [If applicable]  
- My findings: [What you discovered during reproduction]

### Solution Approach
**Analysis:**  
[Your analysis of the root cause]

**Proposed Solution:**  
[High-level description of your fix approach]

**Implementation Plan:**  
1. Update `settings.py` to use Django's built-in CSP functionality and 
   remove the `csp` module  
2. Add missing PayPal domains to CSP allow list  
3. Add nonces to templates using inline `<script>` and `<style>` tags  
4. Handle `style` attributes baked into templates  

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
