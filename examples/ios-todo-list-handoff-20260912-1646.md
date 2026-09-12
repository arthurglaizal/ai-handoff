# AI Handoff: iOS Todo List

Generated: 2026-09-12 16:46 +02:00
Source: Claude Code
Git: feature/local-reminders @ 7c3a91e, uncommitted changes

## Goal

Build a simple native iOS task manager where users can create, edit, complete, and delete tasks. The current focus is adding an optional due date and a local reminder without making task creation slower.

## Current state

- The SwiftUI app can create, edit, complete, and delete tasks.
- Tasks persist locally with SwiftData and remain available after restarting the app.
- Due-date selection is implemented in the task editor.
- Local notification support has been started but is not complete. Permission can be requested and a reminder can be scheduled, but editing or deleting a task does not yet update the pending notification.
- The working tree contains modifications to the task editor and notification service, plus one untracked test file.
- `xcodebuild test -scheme TodoList -destination 'platform=iOS Simulator,name=iPhone 17'` passed 18 existing tests. Notification behavior has not been manually verified on a physical device.

## Key context

- The minimum supported version is iOS 17, so the project uses SwiftData rather than Core Data.
- Notification logic should stay outside the SwiftUI views. An earlier attempt scheduled reminders directly from `TaskEditorView`, but it made edit and cancellation behavior difficult to control. The current direction is to keep this logic in `NotificationService`.
- A reminder should only be scheduled when the task is incomplete and its due date is in the future.
- Keep the interface small and native. Do not add categories, priorities, accounts, or cloud synchronization in this phase.

## Relevant files

- `TodoList/Models/TodoItem.swift`: SwiftData task model, including the optional due date.
- `TodoList/Views/TaskEditorView.swift`: form used to create and edit tasks.
- `TodoList/Services/NotificationService.swift`: notification permission, scheduling, and cancellation logic.
- `TodoList/Views/TaskListView.swift`: completion and deletion actions that still need to notify the service.
- `TodoListTests/NotificationServiceTests.swift`: untracked tests started for reminder identifiers and future-date validation.

## Next steps

1. Finish `NotificationService` so a reminder uses the task UUID as its notification identifier and can be replaced or cancelled reliably.
2. Connect task editing, completion, and deletion to the corresponding scheduling or cancellation method.
3. Complete the notification service tests, then rerun the full test scheme.
4. Verify permission, scheduling, editing, completion, and deletion on a physical iPhone.

## Open issues

- Decide whether clearing a due date should also clear the reminder toggle or simply disable it.
- The final notification wording has not been chosen. The current placeholder uses the task title as the notification body.
