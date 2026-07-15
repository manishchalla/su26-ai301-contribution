# Contribution #2: Manually adjusted column widths aren't retained after relaunch

**Contribution Number:** 2  
**Student:** Manish Challa  
**Issue:** https://github.com/adamgell/cmtraceopen/issues/255  
**Status:** Phase I – Complete

---

## Why I Chose This Issue

I chose this issue because it is a well-defined desktop application bug with clear reproduction steps and a realistic scope for an open-source contribution. Unlike issues that require major architectural changes or extensive domain knowledge, this bug appears to be localized to the application's UI state persistence logic, making it an excellent opportunity to understand an existing production codebase while contributing a meaningful fix.

This issue also aligns with my goal of improving my debugging, code investigation, implementation, testing, and pull request workflow skills. My previous contribution primarily involved adding project content, whereas this contribution requires reproducing a real software defect, investigating its root cause, implementing a production fix, validating the solution, and collaborating through the complete GitHub contribution process.

---

# Understanding the Issue

## Problem Description

The application allows users to manually resize table columns while viewing log files. However, after closing and reopening the application, the manually adjusted column widths are lost and revert back to their automatically calculated default values.

This behavior makes it inconvenient for users who regularly customize their workspace because their preferred column layout is not preserved across application sessions.

## Expected Behavior

The application should persist manually resized column widths when it closes and restore those widths automatically when the application is launched again.

## Current Behavior

Column widths can be adjusted successfully during runtime. However, after restarting the application and reopening the same log file, all manually configured widths are reset to their default values.

## Affected Components

Based on the issue description and the initial repository investigation, the affected functionality is expected to involve:

- UI state persistence
- Column width management
- User preferences
- Table/Grid rendering
- Application startup
- Application initialization

The exact source files and methods will be confirmed during Phase II.

---

# Reproduction Process

## Environment Setup

The repository was forked and assigned to me by the repository maintainer. I cloned my fork locally and configured the project on Windows 11.

The project uses:

- React 19
- TypeScript
- Rust
- Tauri
- Zustand

Development environment:

- Windows 11
- Node.js v22.19.0
- npm v11.12.1
- Rust v1.97.0
- Cargo v1.97.0
- VS Code

Project setup steps completed:

```bash
npm ci
npm run build
npm run app:dev
```

Initially, the desktop application could not start because Cargo was unavailable from the terminal. After verifying the Rust installation and restarting the development environment, Cargo was detected successfully and the application launched correctly.

The desktop application was then used to reproduce the reported issue.

## Steps to Reproduce

1. Launch the application using `npm run app:dev`.
2. Open a valid CMTrace formatted log file.
3. Verify that the structured log parser is being used.
4. Manually resize one or more table columns.
5. Close the application completely.
6. Relaunch the application.
7. Open the same log file again.
8. Observe that the manually resized columns return to their default widths.

## Reproduction Evidence

### Commit Showing Reproduction

Phase I documentation will be committed to the AI301 contribution repository.

### Screenshots

The following screenshots were captured during reproduction:

- Initial application layout
- Columns after manual resizing
- Application restarted
- Column widths reset after reopening

*(Screenshots will be added to the repository under `/screenshots`.)*

### My Findings

The issue was successfully reproduced on Windows 11.

Column resizing functions correctly during the active session. However, after restarting the application, every manually adjusted column width is lost and the application restores the default automatically calculated widths instead of the user-defined widths.

---

# Solution Approach

## Analysis

The reported issue was successfully reproduced locally.

The application correctly updates column widths while the application is running, indicating that runtime state management functions as expected.

A preliminary inspection suggests that the application already includes a persistence mechanism for UI preferences through a Zustand store. However, the resized column widths are either:

- not being written to persistent storage, or
- being overwritten during application startup or log initialization.

The exact root cause has **not** yet been confirmed. This investigation will continue during Phase II before any production code is modified.

## Proposed Solution

During Phase II, I will trace the complete lifecycle of column widths to determine:

- where widths are initialized,
- where resize events update the state,
- where values are persisted,
- where they are restored,
- whether they are unintentionally reset during startup.

Once the exact root cause is confirmed, I will implement a minimal fix that preserves manually resized column widths across application restarts without affecting the existing automatic sizing behavior.

## Implementation Plan

Using the UMPIRE framework:

### Understand

Understand how column widths are calculated, updated, saved, restored, and reset throughout the application lifecycle.

### Match

Look for similar persistence mechanisms already used by the application for:

- Window size
- Theme
- Recent files
- Other UI preferences

### Plan

1. Trace the complete column width lifecycle.
2. Identify where persistence occurs.
3. Confirm the root cause.
4. Implement the fix.
5. Add or update automated tests.
6. Perform manual verification.
7. Submit the Pull Request.

### Implement

Implementation will begin after the root cause has been confirmed during Phase II.

### Review

- Follow project coding standards.
- Keep the implementation minimal.
- Preserve existing behavior.
- Add regression tests if necessary.

### Evaluate

Verify that manually resized column widths remain unchanged after restarting the application while ensuring automatic sizing continues to function for first-time users.

---

# Testing Strategy

## Unit Tests

- [ ] Verify manually resized widths are saved.
- [ ] Verify saved widths are restored after restart.
- [ ] Verify default sizing works when no saved settings exist.

## Integration Tests

- [ ] Resize multiple columns.
- [ ] Restart the application.
- [ ] Verify persistence across multiple log files.

## Manual Testing

Manual testing was completed during Phase I.

The application launched successfully, a structured CMTrace log was opened, multiple columns were resized, the application was restarted, and the same log file was reopened.

The manually adjusted column widths reverted to their default values, successfully reproducing the reported issue.

---

# Implementation Notes

## Week 1 Progress

- Selected GitHub Issue #255.
- Requested assignment from the repository maintainer.
- Received assignment.
- Forked the repository.
- Cloned the repository locally.
- Configured the development environment.
- Installed project dependencies.
- Installed and verified Rust and Cargo.
- Successfully built the frontend.
- Successfully launched the desktop application.
- Created and opened a valid structured CMTrace log.
- Successfully reproduced the reported issue.
- Captured reproduction evidence.
- Completed Phase I investigation.

## Week 2 Progress

To be updated during Phase II and implementation.

## Code Changes

**Files Modified:** None (Phase I)

**Key Commits:** Pending

**Approach Decisions:**

Implementation decisions will be documented after the Phase II investigation confirms the root cause.

---

# Pull Request

**PR Link:** Pending

## PR Description

Will be prepared after implementation and testing are completed.

## Maintainer Feedback

Pending.

## Status

Not yet submitted.

---

# Learnings & Reflections

## Technical Skills Gained

During Phase I, I gained experience configuring and running a desktop application built using React, TypeScript, Rust, Tauri, and Zustand.

I also improved my understanding of reproducing UI persistence issues, documenting software defects, analyzing an unfamiliar codebase before implementation, and preparing evidence for an open-source contribution.

## Challenges Overcome

The first challenge was configuring the desktop development environment. Initially, the application failed to launch because Cargo was unavailable to the development terminal. After verifying the Rust installation and restarting the environment, the application launched successfully.

The second challenge was creating a valid CMTrace formatted log file. My initial test log was interpreted as plain text, preventing the issue from being reproduced. After creating a properly formatted structured log, the application parsed it correctly and the reported bug was successfully reproduced.

## What I'd Do Differently Next Time

Next time, I would spend additional time understanding the repository architecture and development workflow before beginning implementation. Doing so would reduce setup time and allow investigation of the production code to begin earlier.

---

# Resources Used

- CMTrace Open Repository
- Repository README
- Repository CONTRIBUTING Guide
- GitHub Issue #255
- Project source code
- Tauri Documentation
- Rust Documentation
- React Documentation
- Zustand Documentation
