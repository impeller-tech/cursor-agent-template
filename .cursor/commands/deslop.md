---
name: deslop
description: "Remove AI-generated code slop from branch by analyzing diff against main. Identifies and removes unnecessary comments, defensive code, type casts, and style inconsistencies introduced by AI assistants."
args:
  - name: base_branch
    description: "Base branch to compare against (default: main)"
    isRequired: false
    default: "main"
  - name: scope
    description: "Scope of analysis (all|staged|modified). 'all' checks all changes, 'staged' only staged files, 'modified' only modified files"
    isRequired: false
    default: "all"
  - name: report_level
    description: "Detail level of report (summary|detailed). 'summary' provides 1-3 sentence overview, 'detailed' lists all changes"
    isRequired: false
    default: "summary"
---

# Remove AI Code Slop

Analyze the diff against the base branch and systematically remove all AI-generated slop introduced in this branch. This command helps maintain code quality by identifying and eliminating patterns that are characteristic of AI-generated code but don't align with human coding practices or project conventions.

## Primary Objectives

Your mission is to:
1. **Identify AI-generated patterns** - Detect code that exhibits telltale signs of AI generation
2. **Preserve intentional changes** - Only remove slop, never legitimate code improvements
3. **Maintain consistency** - Ensure changes align with existing codebase style and patterns
4. **Report clearly** - Provide a concise summary of what was changed and why

## Step-by-Step Process

### Step 1: Get the Diff

First, identify what has changed in this branch compared to the base branch:

```bash
# Get diff against base branch
git diff {{base_branch}}...HEAD
```

If `scope` is specified:
- `staged`: Use `git diff --cached`
- `modified`: Use `git diff HEAD`
- `all`: Use full diff as above

### Step 2: Analyze Each Changed File

For each file in the diff, examine:

1. **File context** - Read the entire file (or relevant sections) to understand:
   - Existing code style and patterns
   - Comment conventions used in the file
   - Error handling patterns
   - Type safety practices
   - Overall code density and verbosity

2. **Identify slop patterns** - Look for these AI-generated indicators:

#### Comment Slop
- **Over-commenting**: Comments that explain obvious code
  ```typescript
  // ❌ AI slop
  // Set the value to 5
  const value = 5;
  
  // ✅ Human code (no comment needed)
  const value = 5;
  ```

- **Inconsistent commenting**: Comments that don't match the file's comment style
  - If the file has no comments, remove all new comments
  - If the file uses JSDoc, convert inline comments to JSDoc
  - If the file uses brief comments, remove verbose explanations

- **Redundant comments**: Comments that repeat what the code clearly shows
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
  
  // ✅ Human code (trust the validation)
  return user.name;
  ```

- **Excessive try/catch blocks** where errors are already handled upstream:
  ```typescript
  // ❌ AI slop (if called from validated context)
  try {
    const result = validatedFunction();
    return result;
  } catch (error) {
    throw error;
  }
  
  // ✅ Human code (trust the validation)
  return validatedFunction();
  ```

- **Defensive checks** that duplicate existing validation:
  - Check if the function is called from a validated context
  - Check if the file already has error handling patterns
  - Remove defensive code that's redundant with existing patterns

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
  
  // ✅ Human code (proper type guard or validation)
  if (isTargetType(data)) {
    const result = data;
  }
  ```

#### Style Inconsistencies
- **Verbose variable names** that don't match file conventions:
  ```typescript
  // ❌ AI slop (if file uses short names)
  const userAccountInformation = getUser();
  
  // ✅ Human code (matches file style)
  const user = getUser();
  ```

- **Inconsistent formatting**:
  - Spacing that doesn't match the file
  - Quote style mismatches (single vs double)
  - Semicolon usage inconsistencies
  - Import organization that doesn't match the file

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
   - Check if similar patterns exist elsewhere in the file (if so, it might be intentional)
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

After making changes:

1. **Check file consistency** - Ensure the file now matches its own style
2. **Verify functionality** - Ensure no legitimate code was removed
3. **Check project conventions** - Reference AGENTS.md if available for project-specific patterns

### Step 5: Generate Report

Based on `report_level`:

**Summary mode** (default):
- Provide 1-3 sentences describing:
  - What types of slop were found
  - How many files were affected
  - Key changes made

Example:
```
Removed excessive comments and unnecessary defensive null checks from 3 files. Fixed 2 type casts by adding proper type definitions. Aligned variable naming with existing file conventions.
```

**Detailed mode**:
- List each file changed
- Describe specific changes in each file
- Explain why each change was made

## Integration with Project Conventions

If AGENTS.md exists in the project:

1. **Reference coding conventions** - Check AGENTS.md for:
   - Comment style guidelines
   - Error handling patterns
   - Type safety requirements
   - Naming conventions

2. **Follow project patterns** - Ensure removed slop doesn't conflict with documented patterns

3. **Respect architectural decisions** - Don't remove code that aligns with documented architecture

## Common Patterns to Remove

### Over-Explanatory Comments
```typescript
// ❌ Remove
// Initialize the counter variable to zero
let counter = 0;

// ✅ Keep (if file has no comments)
let counter = 0;

// ✅ Keep (if comment explains why, not what)
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
  // ... rest of function
}

// ✅ Keep (if this is an entry point)
function processUser(user: User | null) {
  if (!user) {
    throw new Error('User is required');
  }
  // ... rest of function
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
- Comments that explain complex business logic
- Defensive code in public APIs or entry points
- Type assertions that are necessary and properly typed
- Code that matches project conventions in AGENTS.md
- Error handling that follows project patterns

**Don't be overly aggressive:**
- If unsure whether something is slop, leave it
- If the pattern exists elsewhere in the file, it's likely intentional
- When in doubt, preserve the code

## Quality Checklist

Before completing, verify:
- ✅ All removed comments were truly unnecessary
- ✅ Defensive code removal doesn't break error handling
- ✅ Type fixes are proper, not just removals
- ✅ Style changes match file conventions
- ✅ No legitimate code was removed
- ✅ Changes align with AGENTS.md if available
- ✅ Report accurately describes changes

## Output Requirements

After processing, provide:

1. **Summary report** (based on `report_level`):
   - Summary: 1-3 sentence overview
   - Detailed: File-by-file breakdown

2. **Confidence level** (if applicable):
   - High: Clear slop patterns removed
   - Medium: Some ambiguous cases left
   - Low: Minimal changes, mostly clean code

Remember: The goal is cleaner, more maintainable code that matches human coding patterns and project conventions, not just removing everything that looks AI-generated.
