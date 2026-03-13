# Product Requirements Document (PRD) - Todo App Upgrade (MVP First)

## 1. Overview

We are upgrading the basic TODO app to improve task planning while keeping the product simple and teachable. The MVP introduces due dates, priority levels, and quick filters so users can identify what needs attention today without expanding backend complexity.

This PRD reflects the final scope agreement from the Sept 17 Slack follow-up, which prioritizes a lean MVP and defers visual overdue highlighting and advanced sorting to Post-MVP.

---

## 2. MVP Scope

- Add task field: dueDate (optional).
- dueDate format: ISO date string in YYYY-MM-DD format.
- Add task field: priority with allowed values P1, P2, P3.
- Default priority to P3 when not provided.
- Add filters: All, Today, Overdue.
- Keep storage local only (no backend or external storage changes).
- Maintain title as a required field.
- Validate dueDate: invalid values are ignored and treated as absent.
- Filter behavior:
- All view includes completed tasks.
- Today view shows incomplete tasks only.
- Overdue view shows incomplete tasks only.

---

## 3. Post-MVP Scope

- Add visual highlighting for overdue tasks.
- Add task sorting rules:
- Overdue tasks first.
- Then priority order P1 to P3.
- Then due date ascending.
- Tasks without due dates last.

---

## 4. Out of Scope

- Notifications.
- Recurring tasks.
- Multi-user support.
- Keyboard navigation enhancements.
- External storage integrations.
