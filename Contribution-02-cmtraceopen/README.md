# Contribution #2: Manually adjusted column widths aren't retained after relaunch

**Contribution Number:** 2  
**Student:** Manish Challa  
**Issue:** https://github.com/adamgell/cmtraceopen/issues/255  
**Status:** Phase I – In Progress

---

## Why I Chose This Issue

I chose this issue because it is a well-defined desktop application bug with clear reproduction steps and a realistic scope for a first open-source code contribution. Unlike issues that require major architectural changes or extensive domain knowledge, this bug appears to be localized to the application's UI state persistence logic, making it suitable for understanding an existing codebase while implementing a production-quality fix.

This issue also aligns with my goal of improving my debugging, code investigation, implementation, and pull request workflow skills. My previous contribution focused primarily on creating a catalog entry, whereas this contribution will involve reproducing a real bug, investigating the root cause, modifying production code, validating the fix, and contributing through the complete GitHub review process.

---

## Understanding the Issue

### Problem Description

The application allows users to manually resize table columns while viewing log files. However, after closing and reopening the application, the manually adjusted column widths are lost and revert back to their automatically calculated default values.

This behavior makes it inconvenient for users who regularly customize column layouts for their workflow because their preferences are not preserved between application sessions.

### Expected Behavior

The application should persist manually resized column widths when it closes and restore those widths the next time the application is launched.

### Current Behavior

Column widths can be adjusted during runtime, but after the application is restarted, all manually configured widths are reset to their default automatically calculated sizes.

### Affected Components

Based on the issue description, the affected functionality is expected to involve:

- Column width persistence
- User settings/preferences
- Window initialization
- Table/Grid rendering
- Application startup logic

The exact source files involved will be identified during Phase II.

---

## Reproduction Process

### Environment Setup

The repository has been forked and assigned to me by the maintainer. The next step is to clone the repository, configure the development environment, build the application locally, and reproduce the reported issue before beginning implementation.

Environment details, build commands, and any setup challenges will be documented after successful local reproduction.

### Steps to Reproduce

1. Launch the application.
2. Open a log file.
3. Manually resize one or more table columns.
4. Close the application.
5. Reopen the application.
6. Observe that the column widths have been reset.

### Reproduction Evidence

- **Commit showing reproduction:** Pending
- **Screenshots/logs:** To be added after reproduction
- **My findings:** Investigation in progress

---

## Solution Approach

### Analysis

Based on the issue description, the problem appears to be related to persistence of user interface state. Either the resized column widths are not being saved when the application exits, or the saved values are not being restored correctly during application startup.

The exact root cause has not yet been identified and will be investigated during Phase II.

### Proposed Solution

Investigate how the application currently stores user preferences and determine where column width values should be persisted. Once the persistence mechanism is identified, modify the implementation so that manually resized widths are saved and restored correctly without affecting existing automatic sizing behavior.

### Implementation Plan

Using the UMPIRE framework:

**Understand:**

Understand how column widths are currently calculated, displayed, saved, and restored.

**Match:**

Look for existing persistence mechanisms already used within the application for other user preferences such as window size, theme, layout, or recent files.

**Plan:**

1. Build and run the application locally.
2. Reproduce the reported issue.
3. Trace the column width persistence flow.
4. Identify the root cause.
5. Implement the fix.
6. Add or update automated tests.
7. Perform manual verification.

**Implement:**

Working branch will be updated as implementation progresses.

**Review:**

- Follow project coding standards.
- Keep changes minimal.
- Avoid breaking existing behavior.
- Add regression tests where appropriate.

**Evaluate:**

Verify that manually resized columns remain unchanged after restarting the application and confirm that automatic sizing continues to function normally.

---

## Testing Strategy

### Unit Tests

- [ ] Verify manually resized widths are saved.
- [ ] Verify saved widths are restored after restart.
- [ ] Verify default sizing still works when no saved settings exist.

### Integration Tests

- [ ] Resize multiple columns and restart application.
- [ ] Open different log files after restart and verify persistence.

### Manual Testing

Manual testing will be completed after implementation by reproducing the original issue and confirming that column widths persist correctly across application restarts.

---

## Implementation Notes

### Week 1 Progress

- Selected the issue.
- Commented on the issue requesting assignment.
- Assigned by the repository maintainer.
- Forked the repository.
- Preparing local development environment.
- Beginning reproduction and investigation.

### Week 2 Progress

To be updated during implementation.

### Code Changes

- **Files modified:** To be determined
- **Key commits:** Pending
- **Approach decisions:** Will be documented after investigation

---

## Pull Request

**PR Link:** Pending

**PR Description:**

Will be prepared after implementation and testing are completed.

**Maintainer Feedback:**

- Pending

**Status:** Not yet submitted

---

## Learnings & Reflections

### Technical Skills Gained

To be documented after implementation.

### Challenges Overcome

To be documented after implementation.

### What I'd Do Differently Next Time

To be documented after implementation.

---

## Resources Used

- Repository README
- GitHub Issue #255
- Project source code
- CONTRIBUTING.md (if applicable)
