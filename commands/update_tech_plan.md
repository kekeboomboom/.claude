---
description: Update document using tech-lead-planner agent
---

# Update Tech Plan Document

Update a document using the tech-lead-planner subagent based on your instructions.

**Usage**: `/update_tech_plan <document_path> <update_instructions>`

**Arguments**:
- `document_path`: Path to the document that needs updating
- `update_instructions`: Specific instructions on what to update in the document

**Example**: `/update_tech_plan ./docs/api.md "Add authentication section with JWT examples"`

---

!Task subagent_type="tech-lead-planner" description="Update document" prompt="Please update the document at {{arg1:document_path}} based on these instructions: {{arg2:update_instructions}}

Read the existing document first to understand its current structure and content. Then make the requested updates while maintaining the document's existing style and format.

Focus on:
- Understanding the current document structure
- Making the specific updates requested
- Maintaining consistency with existing content
- Following the document's established patterns and formatting"
