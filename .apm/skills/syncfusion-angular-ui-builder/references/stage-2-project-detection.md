# Stage 2: Project Detection

**Purpose:** Auto-detect project structure, framework, language, and configuration to ensure generated code integrates seamlessly.

**AI Should Auto-Detect:**

1. **Framework Type**
   - Scan for: `package.json`, `angular.json`, `tsconfig.json`, `.angular-cli.json`
   - Detect: Angular version, Standalone components vs NgModule, Angular CLI project
   
2. **Language Preference**
   - Check for: `tsconfig.json` → TypeScript enabled
   - Check for: `.js` vs `.ts` files in src/
   - Default: TypeScript if tsconfig.json exists
   
3. **CSS Strategy**
   - Check for: `tailwind.config.js` → Tailwind CSS
   - Check for: CSS Modules in imports
   - Default: CSS Modules
   
4. **Component Directory**
   - Common paths: `src/app/components/`, `src/components/`, `app/`
   - Find existing component patterns (*.component.ts files)
   
5. **Formatting Rules**
   - Read `.prettierrc` or `prettier.config.js` for indent, quotes, semicolons
   - Read `.eslintrc` for linting rules
   - Apply same rules to generated code
   
6. **Syncfusion License & Package Versioning**
   - Check: Is `SYNCFUSION_LICENSE_KEY` in `.env.local`?
   - Check: Does project already call `registerLicense()`?
   - Prompt: If missing, ask user for license key
   
7. **Syncfusion Package Version Detection**
   - **Scan `package.json` for existing Syncfusion packages:**
     - If `@syncfusion/ej2-angular-*` exists: Extract version (e.g., `23.1.36`)
     - Use SAME version for all new Syncfusion packages → Prevents version conflicts
   - **If NO existing Syncfusion packages found:**
     - Use `*` (latest) version for all new packages: `@syncfusion/ej2-angular-grids@*`
   - **Document version decision:** Log detected version in stage output
   
**Output:**
Show detected settings:
```
✓ Framework: Angular 17 (Standalone Components)
✓ Language: TypeScript (strict mode)
✓ CSS: CSS Modules
✓ Component Dir: src/app/components/
✓ Formatting: 2 spaces, no semicolons
✓ Syncfusion Version: 23.1.36 (detected from package.json)
  OR
✓ Syncfusion Version: * (latest - no existing packages)
