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
   - What packages are already installed?
   - Extract the **major version** from any existing `@syncfusion/ej2-angular-*` package (e.g., `33.2.5` → major is `33`)
   - Any version conflicts?

4. **Resolve Conflicts:**
   - If Syncfusion package already installed:
     - Is version compatible?
     - Suggest upgrade if needed
   - If peer dependencies conflict:
     - Recommend resolution (upgrade, downgrade, or compromise)

5. **Syncfusion Install Version Strategy (MANDATORY):**
   - **If existing Syncfusion packages found in package.json:**
     - Extract the major version number only (e.g., `33.2.5` → use `33`)
     - Install ALL new Syncfusion packages using major version (e.g., `@syncfusion/ej2-angular-schedule@33`) 
     - This avoids patch-not-found errors since not all packages publish every patch version
     - **Never mix major versions** — all Syncfusion packages must share the same major number
   - **If NO existing Syncfusion packages found:**
     - Use `*` (latest) for all new packages: `@syncfusion/ej2-angular-schedule`

6. **Prepare Installation Command:**
   - Generate npm/yarn/pnpm install command using the version strategy from Step 5
   - List packages to add
   - List packages to upgrade (if needed)

**Example Output:**

```
✓ Dependency Analysis

Syncfusion Version Detected: 33.2.5 → installing new packages at @33

New Packages to Install:
  - @syncfusion/ej2-angular-inputs@33
  - @syncfusion/ej2-angular-buttons@33

Existing Packages:
  ✓ @angular/core@17.0.0 (compatible)
  ✓ @angular/common@17.0.0 (compatible)

Conflicts: None

Install Command:
$ npm install @syncfusion/ej2-angular-inputs@33 @syncfusion/ej2-angular-buttons@33

Alternatively with yarn:
$ yarn add @syncfusion/ej2-angular-inputs@33 @syncfusion/ej2-angular-buttons@33

Or with pnpm:
$ pnpm add @syncfusion/ej2-angular-inputs@33 @syncfusion/ej2-angular-buttons@33
 
```

**User Interaction:**

User confirms npm install or does it manually:

```
Ready to install dependencies?
[Install] [Show Command] [Skip]
```

**Status:** AI detects and prepares. User decides whether to install now or later.