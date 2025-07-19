---
allowed-tools: Bash(mkdir:*), Bash(ls:*), WriteToFile(*), ReadFromFile(*)
description: Generate comprehensive documentation for a feature and set it as the current active feature
---

# Feature Documentation Generator

## Context

- Current project structure: !`find . -type f -name "*.md" | head -20`
- Existing documentation: !`ls -la docs/ 2>/dev/null || echo "No docs directory found"`
- Current git branch: !`git branch --show-current 2>/dev/null || echo "Not in a git repository"`
- Current active feature: !`cat docs/current-feature.txt 2>/dev/null || echo "No current feature set"`

## Your Task

Generate comprehensive documentation for the following feature: **$ARGUMENTS**

Create a new folder in the `docs/03-features/` directory to hold the documentation for this feature and create the following files:

### 1. Requirements Document (requirements.md)

Create a requirements document with:

**Section 1 - Introduction:**

- Start with an introduction explaining what we are trying to achieve
- Provide context about the feature and its purpose
- Explain how this new feature fits into the broader project goals

Example format:

```
# Requirements Document

## Introduction

This feature implements a Gmail link aggregator application that connects to a user's Gmail account, extracts links from emails sent to themselves, and provides a web interface to manage and visit these links. The system consists of a Rust backend for Gmail integration and data management, and a Next.js/React frontend for user interaction.
```

**Section 2 - Requirements:**

- Break down the feature into specific requirements
- Each requirement should follow this format:
  - **Requirement N:** Brief description of the requirement
  - **User Story:** As a [user], I want [feature] so that [benefit]
  - **Acceptance Criteria:** List of acceptance criteria in the format "WHEN [condition] THEN the system SHALL [expected outcome]"

Example format:

```
### Requirement 1

**User Story:** As a user, I want to connect my Gmail account to the application, so that I can access emails I've sent to myself containing links.

#### Acceptance Criteria

1. WHEN the user initiates Gmail authentication THEN the system SHALL redirect to Google OAuth2 authorization flow
2. WHEN the user grants permission THEN the system SHALL store the authentication tokens securely
3. WHEN authentication expires THEN the system SHALL automatically refresh tokens using the refresh token
4. IF authentication fails THEN the system SHALL display an appropriate error message and allow retry
```

### 2. Design Document (design.md)

Create a design document with:

**Overview:**

- Provide a high-level overview of the design approach
- Explain the architectural decisions and rationale

**Architecture:**

- **High-Level Architecture Diagram:** Include a mermaid diagram showing the main components and their interactions
- **Core Components:** Describe the core components involved in the implementation
  - Number each component for easy reference
  - Include high-level code snippets to illustrate the design
  - Show interfaces and key data structures

**Components and Interfaces:**

- Detail the interfaces between components
- Show code examples of key structs, traits, and functions

**Data Models:**

- Define the data structures used in the implementation
- Show relationships between different data types

**Error Handling:**

- Define error types and error handling strategies
- Show how errors propagate through the system

**Performance Considerations:**

- Discuss performance implications of the design
- Identify potential bottlenecks and optimization strategies

**Security Considerations:**

- Address security aspects of the implementation
- Document any security measures or concerns

### 3. Tasks Document (tasks.md)

Create a tasks document with:

**Implementation Plan:**

- Break down the implementation into phases and tasks
- Use a hierarchical checkbox format for tracking progress
- Cross-reference requirements for each task using format: `_Requirements: X.Y, Z.A_`

Example format:

```
# Implementation Plan

- [ ] 1. Set up project structure and core interfaces

  - Create Rust backend project with Cargo.toml dependencies (axum, sqlx, tokio, serde, anyhow, thiserror)
  - Create Next.js frontend project with TypeScript and Tailwind CSS
  - Define core data structures and interfaces for User, Link, Email, and SyncStatus models
  - Set up database connection utilities and migration system
  - _Requirements: 3.1, 3.2, 3.3_

- [ ] 2. Implement database schema and models

  - Create SQLite database schema with tables for users, auth_tokens, emails, links, and sync_status
  - Implement Rust structs with SQLx derive macros for database operations
  - Create database migration scripts and initialization logic
  - Write unit tests for database model serialization and basic CRUD operations
  - _Requirements: 3.1, 3.2, 3.3_
```

## Instructions

1. **First, create the directory structure:**

   ```bash
   mkdir -p docs/03-features/<feature-directory>
   ```

2. **Set this as the current active feature:**

   Write the new feature path to `/docs/current-feature.txt`:

   ```
   docs/03-features/<feature-directory>
   ```

3. **Analyze the feature** and break it down into logical components

4. **Analyze existing code if applicable** to inform the design and requirements

5. **Generate each document** following the specified format and structure

6. **Ensure cross-references** between documents are accurate and helpful

7. **Use consistent naming** and numbering throughout all documents

8. **Include practical examples** and code snippets where appropriate

9. **Make sure the documentation is actionable** and provides clear guidance for implementation and acceptance criteria

10. **Create initial commit** for the new feature documentation:
    ```bash
    git add docs/03-features/<feature-directory>/ docs/current-feature.txt
    git commit -m "Initialize feature documentation for <feature-name>"
    ```

### **Expected Output:**

```
## Feature Documentation Created

**Feature Directory**: docs/03-features/<feature-directory>
**Active Feature Set**: Updated /docs/current-feature.txt

**Generated Files**:
- requirements.md (X requirements defined)
- design.md (Y components specified)
- tasks.md (Z tasks planned)

**Next Steps**:
- Use `task-next` command to begin implementation
- Review and refine requirements as needed
- Start with the first task in the implementation plan
```

The documentation should be comprehensive enough that a developer can understand the full scope of the feature and begin implementation based on the provided specifications. After running this command, the new feature will be set as the active feature and ready for task management with the `task-next` command.
