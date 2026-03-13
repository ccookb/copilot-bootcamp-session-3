# Epics and Story Titles - Todo App Upgrade

## MVP

### Epic 1: Task Data Model Enhancements
#### Story: Add optional dueDate field to tasks
##### Technical Requirements
- The system must allow tasks to be saved without a dueDate.
- The system must store dueDate when a valid value is provided on create or update.

##### Acceptance Criteria
- Given a task is created, when dueDate is not provided, then the task is saved successfully with no dueDate value.
- Given a task is created or updated, when a valid dueDate is provided, then the dueDate is stored with that task.

#### Story: Enforce ISO YYYY-MM-DD format handling for dueDate
##### Technical Requirements
- The system must accept dueDate values only in YYYY-MM-DD format.
- The system must treat non-ISO dueDate values as absent.

##### Acceptance Criteria
- Given a dueDate value matches YYYY-MM-DD, when the task is saved, then the dueDate is stored as provided.
- Given a dueDate value does not match YYYY-MM-DD, when the task is saved, then the dueDate is treated as absent.

#### Story: Add priority enum field with values P1, P2, and P3
##### Technical Requirements
- The system must support task priority values P1, P2, and P3 only.
- The system must persist and display the accepted priority value.

##### Acceptance Criteria
- Given a task is created or updated, when priority is provided, then only P1, P2, or P3 are accepted values.
- Given an accepted priority value is provided, when the task is displayed, then the stored priority is shown unchanged.

#### Story: Default priority to P3 when no priority is provided
##### Technical Requirements
- The system must assign P3 as the default priority when priority is omitted.

##### Acceptance Criteria
- Given a new task is created without a priority, when the task is saved, then priority is set to P3.

#### Story: Keep title as a required task field
##### Technical Requirements
- The system must require a non-empty title for task creation.
- The system must block task creation when title is missing.

##### Acceptance Criteria
- Given a user attempts to create a task without a title, when saving, then the task is not created.
- Given a task has a non-empty title, when saving, then the task is created successfully.

#### Story: Ignore invalid dueDate values as absent
##### Technical Requirements
- The system must not persist invalid dueDate values.
- The system must treat tasks with invalid dueDate input as undated for filtering behavior.

##### Acceptance Criteria
- Given an invalid dueDate is entered, when the task is saved, then no dueDate is stored for that task.
- Given a task with an invalid dueDate was saved, when filtered by Today or Overdue, then the task behaves like an undated task.

### Epic 2: Task Filters and Views
#### Story: Add All tasks filter
##### Technical Requirements
- The system must provide an All filter option.
- The All filter must show all tasks regardless of dueDate or completion state.

##### Acceptance Criteria
- Given tasks exist, when All is selected, then all tasks are shown regardless of dueDate.
- Given tasks exist, when All is selected, then both completed and incomplete tasks are shown.

#### Story: Add Today tasks filter
##### Technical Requirements
- The system must provide a Today filter option.
- The Today filter must include only incomplete tasks with dueDate equal to the current date.

##### Acceptance Criteria
- Given tasks exist, when Today is selected, then only tasks with dueDate equal to the current date are eligible to display.
- Given Today is selected, then only incomplete tasks are displayed.

#### Story: Add Overdue tasks filter
##### Technical Requirements
- The system must provide an Overdue filter option.
- The Overdue filter must include only incomplete tasks with dueDate earlier than the current date.

##### Acceptance Criteria
- Given tasks exist, when Overdue is selected, then only tasks with dueDate earlier than the current date are eligible to display.
- Given Overdue is selected, then only incomplete tasks are displayed.

#### Story: Show completed tasks in All view
##### Technical Requirements
- The All filter must include completed tasks.

##### Acceptance Criteria
- Given completed tasks exist, when All is selected, then completed tasks are visible in the list.

#### Story: Hide completed tasks in Today view
##### Technical Requirements
- The Today filter must exclude completed tasks.

##### Acceptance Criteria
- Given completed tasks have dueDate equal to today, when Today is selected, then those completed tasks are not visible.

#### Story: Hide completed tasks in Overdue view
##### Technical Requirements
- The Overdue filter must exclude completed tasks.

##### Acceptance Criteria
- Given completed tasks are overdue, when Overdue is selected, then those completed tasks are not visible.

### Epic 3: Local-Only MVP Delivery
#### Story: Persist task updates using local storage only
##### Technical Requirements
- The system must persist task create, update, and completion changes in local storage.
- The system must preserve task data after page refresh without requiring network access.

##### Acceptance Criteria
- Given a user creates, updates, or completes a task, when the app is refreshed, then changes remain available from local storage.
- Given network connectivity is unavailable, when managing tasks, then core task actions still work using local storage.

#### Story: Deliver MVP without backend or external storage changes
##### Technical Requirements
- MVP implementation must not require backend API integration.
- MVP implementation must not use external storage services.

##### Acceptance Criteria
- Given the MVP implementation is complete, then no backend API integration is required for task CRUD or filtering.
- Given the MVP implementation is complete, then no external storage service is used for task data.

## Post-MVP

### Epic 4: Overdue Visual Treatment
#### Story: Visually highlight overdue tasks
##### Technical Requirements
- The system must apply a distinct visual style to incomplete overdue tasks.
- The system must not apply overdue styling to completed or non-overdue tasks.

##### Acceptance Criteria
- Given a task is incomplete and overdue, when shown in task lists, then it is visually highlighted.
- Given a task is not overdue or is completed, when shown in task lists, then overdue highlight styling is not applied.

### Epic 5: Advanced Task Sorting
#### Story: Sort overdue tasks before non-overdue tasks
##### Technical Requirements
- Sorting must prioritize overdue tasks ahead of non-overdue tasks.

##### Acceptance Criteria
- Given a mixed list of overdue and non-overdue tasks, when sorting is applied, then overdue tasks appear before non-overdue tasks.

#### Story: Sort tasks by priority from P1 to P3
##### Technical Requirements
- For tasks in the same overdue grouping, sorting must order priority as P1, then P2, then P3.

##### Acceptance Criteria
- Given tasks within the same overdue grouping, when sorting is applied, then tasks are ordered by priority P1, then P2, then P3.

#### Story: Sort tasks by due date in ascending order
##### Technical Requirements
- For tasks with the same overdue grouping and priority, sorting must place earlier due dates first.

##### Acceptance Criteria
- Given tasks with the same overdue grouping and priority, when sorting is applied, then earlier due dates appear before later due dates.

#### Story: Place tasks without due dates at the end of sorted results
##### Technical Requirements
- Sorting must place undated tasks after dated tasks within the sorted set.

##### Acceptance Criteria
- Given tasks with and without dueDate in the same sorted set, when sorting is applied, then tasks without dueDate appear after tasks with dueDate.
