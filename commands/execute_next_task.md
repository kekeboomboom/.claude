---
description: Execute the next pending task from a tech-lead-planner implementation document using fullstack-developer agent
allowed_tools: ["Read", "Edit", "Task", "Grep", "Bash"]
---

# Execute Next Task

Execute the next pending task from a tech-lead-planner implementation document using the fullstack-developer agent, then update the document to mark the task as completed.

**Usage**: `/execute_next_task <document_path>`

**Arguments**:
- `document_path`: Path to the tech-lead-planner implementation document containing numbered tasks

**Example**: `/execute_next_task ./docs/user-profile-implementation.md`

---

!Read file_path="{{arg1:document_path}}"

# Parse the document to find the task list and next pending task

!Grep pattern="^## Task List for Fullstack Developer" path="{{arg1:document_path}}" output_mode="content" -n

!Grep pattern="^\d+\.\s\*\*" path="{{arg1:document_path}}" output_mode="content" -n -A 5

# Find the first task that doesn't have a ✅ completion marker
# Task format: "1. **Backend** - Description..."
# Completed format: "1. **Backend** - Description... ✅ *Completed: timestamp*"

!Task subagent_type="general-purpose" description="Find next pending task" prompt="Please analyze the document at {{arg1:document_path}} and identify the next pending task that needs to be executed.

Looking for:
1. A numbered task list section (usually titled '## Task List for Fullstack Developer')
2. Tasks in format: '1. **Backend** - Description...' or similar
3. Find the first task that does NOT have a ✅ completion marker
4. Extract the complete task description including:
   - Task number
   - Task type (Backend/Frontend/Database/Testing/etc.)
   - Full description
   - Files to modify (if listed)
   - Pattern to follow (if listed)
   - Success criteria (if listed)

If all tasks are completed, report that. If no task list is found, report that as well.

Return the task information in this format:
```
TASK_NUMBER: [number]
TASK_TYPE: [Backend/Frontend/etc.]
TASK_DESCRIPTION: [full description]
TASK_FILES: [files to modify]
TASK_PATTERN: [pattern to follow]
TASK_SUCCESS: [success criteria]
STATUS: [FOUND/ALL_COMPLETED/NO_TASK_LIST]
```"

# If a pending task is found, execute it with fullstack-developer
!Task subagent_type="fullstack-developer" description="Execute the identified task" prompt="Execute the following task from the implementation document:

**Task Details:**
- Document: {{arg1:document_path}}
- Task to execute: The task identified by the previous analysis

**Instructions:**
1. Read the implementation document to understand the full context
2. Locate the specific task that was identified as next pending
3. Execute that task following the provided:
   - Files to modify
   - Patterns to follow
   - Success criteria
4. Implement the required changes with high code quality
5. Run any verification steps (linting, testing) as specified
6. Report completion with a brief summary of what was implemented

Focus on executing ONLY the identified task, not the entire task list. Follow the established patterns and ensure the implementation meets the success criteria."

# After successful execution, update the document to mark the task as completed
!Task subagent_type="general-purpose" description="Update document with completion status" prompt="Please update the document at {{arg1:document_path}} to mark the recently executed task as completed.

**Instructions:**
1. Read the current document
2. Find the task that was just executed (the first one without ✅ marker)
3. Add a completion marker to that task in this format:
   - Add ✅ at the end of the task description line
   - Add a new line with: *Completed: [current timestamp] - [brief summary]*

**Example transformation:**
Before:
```
1. **Backend** - Modify `src/api/users.js` to add new getUserProfile endpoint following existing pattern
```

After:
```
1. **Backend** - Modify `src/api/users.js` to add new getUserProfile endpoint following existing pattern ✅
   *Completed: 2024-01-15 14:30 - Added getUserProfile endpoint with proper error handling*
```

Preserve all other content and formatting in the document."

# Provide user feedback
echo "✅ Task execution completed!"
echo ""
echo "📋 Next steps:"
echo "- Review the changes made by the fullstack-developer agent"
echo "- Run tests if needed: npm test (or appropriate test command)"
echo "- Run /execute_next_task {{arg1:document_path}} again to continue with the next task"
echo ""
echo "📄 Document updated: {{arg1:document_path}}"