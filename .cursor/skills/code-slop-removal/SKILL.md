---
name: code-slop-removal
description: "Guide for removing AI-generated code slop. Use when cleaning up AI-generated code, removing unnecessary comments, defensive code, type casts, or style inconsistencies."
---

# Code Slop Removal Guide

Systematic approach to identifying and removing AI-generated code patterns that don't align with human coding practices.

## Quick Start

Analyze diff against base branch, identify AI-generated slop patterns, remove while preserving intentional changes, maintain consistency with existing codebase.

## Primary Objectives

1. **Identify AI-generated patterns** - Detect telltale signs of AI generation
2. **Preserve intentional changes** - Only remove slop, never legitimate improvements
3. **Maintain consistency** - Align with existing codebase style and patterns
4. **Report clearly** - Provide concise summary of changes

## Step-by-Step Process

### Step 1: Get the Diff

```bash
# Get diff against base branch
git diff {{base_branch}}...HEAD
```

If `scope` is specified:
- `staged`: Use `git diff --cached`
- `modified`: Use `git diff HEAD`
- `all`: Use full diff as above

### Step 2: Analyze Each Changed File

For each file, examine:

1. **File context** - Read entire file to understand:
   - Existing code style and patterns
   - Comment conventions
   - Error handling patterns
   - Type safety practices
   - Code density and verbosity

2. **Identify slop patterns**:

#### Comment Slop
- **Over-commenting**: Comments explaining obvious code
  ```typescript
  // ❌ AI slop
  // Set the value to 5
  const value = 5;
  
  // ✅ Human code
  const value = 5;
  ```

- **Inconsistent commenting**: Comments that don't match file's style
  - If file has no comments, remove all new comments
  - If file uses JSDoc, convert inline comments to JSDoc
  - If file uses brief comments, remove verbose explanations

- **Redundant comments**: Comments repeating what code shows
  ```typescript
  // ❌ AI slop
  // This function returns the user's name
  function getName() {
    return user.name;
  }
  ```

#### Defensive Code Slop
- **Unnecessary null checks** in trusted/validated code paths:
  ```typescript
  // ❌ AI slop (if user is already validated)
  if (user && user.name) {
    return user.name;
  }
  
  // ✅ Human code
  return user.name;
  ```

- **Excessive try/catch blocks** where errors handled upstream:
  ```typescript
  // ❌ AI slop
  try {
    const result = validatedFunction();
    return result;
  } catch (error) {
    throw error;
  }
  
  // ✅ Human code
  return validatedFunction();
  ```

#### Type Safety Slop
- **Casts to `any`** to bypass type issues:
  ```typescript
  // ❌ AI slop
  const value = (someValue as any).property;
  
  // ✅ Human code (proper typing)
  interface ValueType {
    property: string;
  }
  const value = (someValue as ValueType).property;
  ```

- **Type assertions without proper types**:
  ```typescript
  // ❌ AI slop
  const result = data as unknown as TargetType;
  
  // ✅ Human code (proper type guard)
  if (isTargetType(data)) {
    const result = data;
  }
  ```

#### Style Inconsistencies
- **Verbose variable names** that don't match file conventions
- **Inconsistent formatting**: spacing, quotes, semicolons, imports
- **Unnecessary abstractions**:
  ```typescript
  // ❌ AI slop
  const getValue = () => value;
  const result = getValue();
  
  // ✅ Human code
  const result = value;
  ```

### Step 3: Apply Fixes

For each identified slop pattern:

1. **Verify it's actually slop**:
   - Check if similar patterns exist elsewhere (might be intentional)
   - Verify it's not required for functionality
   - Confirm it doesn't match project conventions from AGENTS.md

2. **Remove or refactor**:
   - Remove unnecessary comments
   - Simplify defensive code
   - Fix type issues properly (don't just remove casts)
   - Align style with file conventions

3. **Preserve legitimate code**:
   - Keep comments that add value (explain "why", not "what")
   - Keep defensive code in untrusted code paths
   - Keep type assertions that are necessary and properly typed
   - Keep style that matches project conventions

### Step 4: Verify Changes

- Check file consistency - matches its own style
- Verify functionality - no legitimate code removed
- Check project conventions - reference AGENTS.md if available

### Step 5: Generate Report

**Summary mode** (default):
- 1-3 sentences describing types of slop found, files affected, key changes

**Detailed mode**:
- List each file changed
- Describe specific changes
- Explain why each change was made

## Common Patterns to Remove

### Over-Explanatory Comments
```typescript
// ❌ Remove
// Initialize the counter variable to zero
let counter = 0;

// ✅ Keep (if comment explains why)
// Start at 0 to match backend indexing
let counter = 0;
```

### Redundant Validation
```typescript
// ❌ Remove (if user is validated upstream)
function processUser(user: User) {
  if (!user) {
    throw new Error('User is required');
  }
  // ...
}

// ✅ Keep (if this is an entry point)
function processUser(user: User | null) {
  if (!user) {
    throw new Error('User is required');
  }
  // ...
}
```

### Type Workarounds
```typescript
// ❌ Remove
const data = (response as any).data;

// ✅ Fix properly
interface ApiResponse {
  data: unknown;
}
const data = (response as ApiResponse).data;
```

## Anti-Patterns to Avoid

**Don't remove:**
- Comments explaining complex business logic
- Defensive code in public APIs or entry points
- Type assertions that are necessary and properly typed
- Code matching project conventions in AGENTS.md
- Error handling following project patterns

**Don't be overly aggressive:**
- If unsure, leave it
- If pattern exists elsewhere in file, likely intentional
- When in doubt, preserve the code

## Integration with Project Conventions

If AGENTS.md exists:
1. Reference coding conventions (comment style, error handling, type safety, naming)
2. Follow project patterns
3. Respect architectural decisions

## Quality Checklist

- ✅ All removed comments were truly unnecessary
- ✅ Defensive code removal doesn't break error handling
- ✅ Type fixes are proper, not just removals
- ✅ Style changes match file conventions
- ✅ No legitimate code was removed
- ✅ Changes align with AGENTS.md if available
- ✅ Report accurately describes changes
