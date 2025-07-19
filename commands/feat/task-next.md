---
allowed-tools: Bash(*), WriteToFile(*), ReadFromFile(*)
description: Intelligently manage task lifecycle - check current task, complete if done, start next logical task
---

# Task Next Command

## Context

- Current feature folder: !`cat docs/current-feature.txt`
- Current git status: !`git status --porcelain`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10`
- Git diff: !`git diff HEAD~1`
- Tasks document: @{!`cat docs/current-feature.txt`}/tasks.md
- Requirements document: @{!`cat docs/current-feature.txt`}/requirements.md
- Design document: @{!`cat docs/current-feature.txt`}/design.md

## Your Task

Intelligently manage task progression: **$ARGUMENTS** (optional task-specific focus)

### Decision Flow:

1. **ANALYZE CURRENT STATE**

   - Parse tasks document to find current active task(s) `[-]`
   - Check git status for uncommitted changes
   - Review recent commits for completion indicators

2. **DETERMINE ACTION BASED ON STATE**

   **State A: Active Task Exists `[-]`**

   - Evaluate if task acceptance criteria are met
   - Check if all required files/functionality are implemented
   - Review git changes since task started

   **If Task is Complete:**

   - Execute completion workflow (State A → Complete → Start Next)

   **If Task is In Progress:**

   - Execute progress tracking workflow (State A → Progress Check)

   **State B: No Active Task `[ ]` available**

   - Find next logical task based on dependencies
   - Execute start workflow (State B → Start Next)

   **State C: All Tasks Complete `[x]`**

   - Generate final project summary
   - Suggest next phase or project cleanup

### Workflow Actions:

#### **COMPLETION WORKFLOW** (when active task is done)

1. **Validate Completion**:

   - Review task description and requirements
   - Verify acceptance criteria are met
   - Check for any missing implementation details

2. **Update Task Status**:

   - Change `[-]` to `[x]` with completion timestamp
   - Add implementation summary
   - List key files modified
   - Reference relevant commits
   - Update parent task/phase progress

3. **Create Completion Commit**:

   - Format: "Complete task {task-number}: {task-description}"
   - Include all remaining changes

4. **Find Next Task**:

   - Identify newly unblocked tasks
   - Select next logical task based on:
     - Dependencies satisfied
     - Critical path priority
     - Phase progression
     - Resource availability

5. **Start Next Task**:
   - Execute start workflow for selected task

#### **PROGRESS TRACKING WORKFLOW** (when active task continues)

1. **Assess Current Progress**:

   - Review what's been implemented so far
   - Identify remaining acceptance criteria
   - Check for any blockers or issues

2. **Update Task Notes**:

   - Add progress summary
   - Document current implementation state
   - Note any discovered dependencies or complications

3. **Plan Next Steps**:

   - Identify specific next actions needed
   - Estimate effort remaining
   - Suggest immediate focus areas

4. **Maintain Branch/Commit Strategy**:
   - Ensure working on appropriate branch
   - Suggest intermediate commits if significant progress made

#### **START WORKFLOW** (when no active task exists)

1. **Select Next Task**:

   - Parse all `[ ]` tasks
   - Filter by dependency requirements
   - Prioritize by:
     - Critical path impact
     - Phase progression
     - Complexity and effort estimates

2. **Prepare Task Context**:

   - Show task acceptance criteria
   - List dependencies and prerequisites
   - Identify likely files to modify

3. **Update Task Status**:

   - Change `[ ]` to `[-]` with start timestamp
   - Update phase progress tracking

4. **Create Working Environment**:
   - Ensure on appropriate branch or create new one
   - Format: `task/{task-number}-{brief-description}`
   - Create start commit: "Start task {task-number}: {task-description}"

### **ADDITIONAL TRANSITIONS TO HANDLE:**

#### **Error Recovery States:**

- **Multiple Active Tasks**: Consolidate or prioritize
- **Orphaned Branches**: Clean up and redirect
- **Conflicting Changes**: Resolve and rebase
- **Missing Dependencies**: Block task and suggest alternatives

#### **Special Conditions:**

- **Hotfix Needed**: Pause current task, handle urgent fix
- **Requirements Changed**: Update affected tasks, re-prioritize
- **Phase Boundary**: Complete phase summary, plan next phase
- **External Blockers**: Mark task as blocked, find alternative work

### **Expected Output Format:**

```
## Task Management Summary

**Current State**: [Active Task Continuing / Task Completed / Starting New Task / All Complete]

**Action Taken**:
- [Detailed description of what was done]

**Task Details**:
- **Current/Completed Task**: X.Y Task Name
- **Status**: [In Progress / Completed / Started]
- **Progress**: [Specific progress indicators]

**Next Steps**:
- [Immediate actionable items]
- [Estimated time to completion]

**Project Status**:
- **Overall Progress**: X/Y tasks completed (Z%)
- **Current Phase**: Phase N (a/b tasks completed)
- **Critical Path**: [On track / Needs attention / Blocked]
```

### **Validation Checks:**

- Ensure no orphaned in-progress tasks
- Verify all completed tasks have proper documentation
- Check that dependencies are respected
- Validate branch and commit strategy alignment
- Confirm requirement references are current

Provide comprehensive summary of actions taken and clear next steps for continued development.
