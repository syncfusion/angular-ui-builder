# Stage 6: Dependencies

**Purpose:** Detect required packages, resolve version conflicts, prepare npm install command.

**AI Should:**

1. **Detect Required Packages:**
   - Scan generated code imports
   - List all @syncfusion/ej2-angular-* packages used
   - Check for other dependencies (@angular/core, @angular/common, etc.)

2. **Validate Package Names Against Skills (CRITICAL):**
   - For each mapped component, read the skill's `getting-started.md`
   - Extract the **authoritative package name** from the skill
   - Compare against what the generated code is actually importing
   - If mismatch found, use the correct package name from the skill
   - This prevents installing wrong packages (e.g., deriving `@syncfusion/ej2-angular-listview` when the correct package is `@syncfusion/ej2-angular-lists`)

3. **Check Project's package.json:**
   - What packages already installed?
   - What versions are currently in use?
   - Any version conflicts?

4. **Resolve Conflicts:**
   - If Syncfusion package already installed:
     - Is version compatible?
     - Suggest upgrade if needed
   - If peer dependencies conflict:
     - Recommend resolution (upgrade, downgrade, or compromise)

5. **Prepare Installation Command:**
   - Generate npm/yarn/pnpm install command
   - List packages to add
   - List packages to upgrade (if needed)

**Example Output:**

```
✓ Dependency Analysis

New Packages to Install:
  - @syncfusion/ej2-angular-inputs (latest)
  - @syncfusion/ej2-angular-buttons (latest)

Existing Packages:
  ✓ @angular/core@17.0.0 (compatible)
  ✓ @angular/common@17.0.0 (compatible)

Conflicts: None

Install Command:
$ npm install @syncfusion/ej2-angular-inputs @syncfusion/ej2-angular-buttons

Alternatively with yarn:
$ yarn add @syncfusion/ej2-angular-inputs @syncfusion/ej2-angular-buttons

Or with pnpm:
$ pnpm add @syncfusion/ej2-angular-inputs @syncfusion/ej2-angular-buttons
```

**User Interaction:**
User confirms npm install or does it manually:
```
Ready to install dependencies?
[Install] [Show Command] [Skip]
```

**Status:** AI detects and prepares. User decides whether to install now or later.
