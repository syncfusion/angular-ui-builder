# Stage 5: Code Generation

**Purpose:** Generate production-ready Angular code, CSS, and TypeScript interfaces with accessibility and web standards compliance.

## CRITICAL: Read Component Skills BEFORE Code Generation

**THIS STEP IS NOT OPTIONAL - Must be completed before writing any code**

### Step 1: Extract All Selected Components and Icons from `component-mapping.json`

Parse `component-mapping.json` and extract all unique Syncfusion components, skills, and icons.

**Display this output BEFORE reading any component skills:**

```
Syncfusion Components: [list unique components]
Skills: [list unique skills]
Icons: [list unique iconCss values]
```

**DO NOT skip or substitute any components with native HTML.**

---

### Step 2: Read Getting-Started for EACH Component Skill

**For every single component skill identified in Step 1:**

1. **Read**: {.agent-root}/skills/<skill-name>/references/getting-started.md

- This is the ONLY authoritative source for imports and setup
- You MUST read the file completely (no skimming)
- Do NOT generate imports without reading this first

**If not found:**

- Check {.agent-root}/skills/<skill-name>/references/*-getting-started.md
- Example: {.agent-root}/skills/<skill-name>/references/dropdownbutton-getting-started.md
- You MUST read the selected file completely
   
2. **Extract and document:**
   - Package name (e.g., `@syncfusion/ej2-angular-grids`)
   - Exact import statement for the component
   - **Style imports (CRITICAL)** - use overall single Syncfusion theme package
   - Required providers/setup (if any)
   - Base dependencies

**Important:** ⚠️ Card is CSS-based (`<div className="e-card">`) and works with proper style references, not a Angular Component import.

### Step 3: If Complex Features Needed

- Read: `{.agent-root}/skills/<skill-name>/SKILL.md` for complete API documentation
- Read feature-specific guides: `<skill-name>/references/filtering.md`, `validation.md`, `customization.md`, etc.

### Step 4: (CRITICAL) Read the Syncfusion themes guide to install the overall single Syncfusion theme package:

1. **Read:** `{.agent-root}/skills/syncfusion-angular-ui-builder/references/syncfusion-themes.md`

**Important** Use overall single Syncfusion theme package.

### Step 5: NOW Generate Code Using Extracted Information

Only after completing Steps 1-4, generate the .ts, .html files using the exact imports from component skills.

**ALL Selected Components MUST Be Used.** Do not substitute Stage 3 components with native HTML alternatives.

**Common Mistake to Avoid:**
❌ Generate code, then try to add overall single Syncfusion theme style imports later → Results in missing styles, broken UI
✅ Read getting-started FIRST, use overall single Syncfusion theme style imports, THEN generate code with all imports included

**Why This Order Is Critical:**
- Component skills contain the authoritative setup syntax
- Style imports are often forgotten and cause broken styling
- Reading first ensures: correct imports, correct styles, no missing dependencies, error-free code
- Compatibility with Syncfusion skill updates

---

## Code Generation Process

**After reading all component skills, AI Should:**

1. **Generate .ts component file with .html template**:
   - Angular component class with lifecycle hooks
   - Proper Syncfusion imports
   - TypeScript interface for component properties
   - Event handlers and state management
   - Error handling and validation
   - WCAG 2.1 AA accessibility markup (ARIA labels, semantic HTML, focus management)
   - JSDoc comments explaining usage
   - **For complex UIs with multiple distinct sections: create separate component files per section, do not combine into one file**

2. **Generate CSS stylesheet** (based on project preference):
   - CSS Style: `.css` with class names
   - Tailwind: Class-based styling
   - Inline: Style objects in component
   - Responsive design: Mobile-first (320px, 768px, 1024px+)
   - Light/dark theme support if needed

3. **Generate TypeScript interfaces**:
   - Props interface with all prop types
   - State types if using hooks
   - Event handler signatures

4. **Reference code standards** from:
   - web-standards.md (accessibility + security rules)
   - Component skill's feature-specific guides (filtering.md, validation.md, styling.md, etc.)

**Code Generation Standards:**

- **Component Imports:** Use exact import syntax from component skill's getting-started.md
- **Style Imports:** Include the Syncfusion single package theme from `references/syncfusion-themes.md`
 **Read:** `{.agent-root}/skills/syncfusion-angular-ui-builder/references/syncfusion-themes.md`
- **Semantic HTML:** Use proper HTML5 elements (`<form>`, `<label>`, `<button>`, etc.)
- **Accessibility:** ARIA labels, roles, aria-describedby, aria-invalid where needed
- **TypeScript:** No `any` types, full type safety
- **Error Handling:** Try-catch blocks, user-friendly error messages
- **Responsive:** Flexbox/Grid layouts, media queries
- **Performance:** OnPush change detection strategy, TrackBy for *ngFor
- **Security:** Use Angular DomSanitizer for dynamic content, sanitize inputs, no hardcoded secrets
- **Comments:** JSDoc on component, explain complex logic
- **Layout Validation (CRITICAL):** For any multi-section layout (sidebar + content, header + body, grid layouts, etc.): (1) Use flexbox for section coordination, (2) Prevent flexible sections from shrinking below content width, (3) Contain main content within viewport to prevent horizontal scroll, (4) Verify all sections properly aligned across mobile (320px), tablet (768px), and desktop (1024px+) viewports

### Media (MANDATORY)

- **Placeholder Images:** Use [Unsplash](https://unsplash.com) for high-quality placeholder images
  - Format: `https://images.unsplash.com/photo-[id]?w=[width]&h=[height]&fit=crop`
  - Example: `https://images.unsplash.com/photo-1560472354-b33ff0c44a43?w=200&h=100&fit=crop`
  - Always specify dimensions (width x height) in the URL
  - Use relevant keywords for context-appropriate images

### Icon Handling (MANDATORY)

**CRITICAL: ALL Icons from Stage 3 Selection List MUST Be Used**

Every icon from the Stage 3 selection list MUST appear in the generated code:
- Navigation icons MUST be used in navigation elements
- Action icons MUST be used for corresponding action buttons
- Data visualization icons MUST be used in chart/grid related UI
- Creation icons MUST be used for add/create actions
- All selected icons MUST be implemented in appropriate UI locations based on their semantic meaning

**Step 1: Attempt to find icon from Component Mapping**
- **Always run ComponentMapper script first** to get semantic icon mappings (BM25 search against EJ2 icons)
- **Use icon CSS class if score > 5:** `<span className="e-icons e-mail"></span>`
- **Never leave empty space** - either icon or emoji, not blank

**Step 2: If Icon Not Found or Score Too Low**
- ❌ DO NOT skip or use empty space
- ✅ Update the element's `icon_hint` in `component-mapping.json`
- ✅ Run the ComponentMapper script again: `node components-search.cjs ../component-mapping.json`
- ✅ Re-check the script output for improved icon match

**Step 3: If Still Not Found**
- ✅ Use emoji fallback: `<span>📧</span>` or appropriate emoji
- Document why icon wasn't found in code comments
- Maintain visual consistency with other components

**Example**:
```json
// Before: icon_hint was too vague
"icon_hint": "email"

// After: updated with more keywords
"icon_hint": "email envelope mail message send"
```

### Button & Icon Styling with Syncfusion (MANDATORY)

**Principle:** Let Syncfusion own button dimensions and styling. Use Tailwind only for layout around buttons.

❌ **INCORRECT** - Overriding Syncfusion button sizes with inline CSS:
```html
<button class="e-control e-btn e-large" style="padding: 1rem; width: 8rem; height: 3rem;">
  <span class="e-icons e-play"></span>
  Play
</button>
```

✅ **CORRECT** - Syncfusion owns button, CSS wrapper owns layout:
```html
<div class="button-group">
  <button class="e-control e-btn e-lib e-large e-primary">
    <span class="e-icons e-video"></span>
    Play
  </button>

  <button class="e-control e-btn e-lib e-large e-outline">
    <span class="e-icons e-circle-info"></span>
    More Info
  </button>
</div>
```

**Why This Works:**
- Syncfusion defines sizing + alignment internally
- Icons align correctly with Syncfusion's design system
- No padding collision or override conflicts
- Consistent appearance across all Syncfusion components

---

### Component Reuse Across UI (Same Component, Multiple Places)

**Principle:** One Syncfusion component type can be reused throughout your UI with customizations. For example, `ButtonComponent` can serve as the Login button, Forgot Password link, and Sign Up button—each customized via CSS variables.

**Example - Button Used in Multiple Places:**
```typescript
// login-form.component.ts
import { Component } from '@angular/core';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
  selector: 'app-login-form',
  templateUrl: './login-form.component.html',
  styleUrls: ['./login-form.component.css'],
  standalone: true,
  imports: [ButtonComponent]
})
export class LoginFormComponent {}
```

```html
<!-- login-form.component.html -->
<!-- All use the same ButtonComponent, but different CSS classes for customization -->
<div class="login-button">
  <button ejs-button isPrimary="true">Login</button>
</div>

<div class="forgot-password">
  <button ejs-button cssClass="e-flat e-small">Forgot Password?</button>
</div>

<div class="sign-up">
  <button ejs-button cssClass="e-outline">Sign Up Here</button>
</div>
```

```css
/* login-form.component.css */
/* Primary button - main CTA */
.login-button .e-btn {
  --bs-primary: #0d6efd;
  width: 100%;
}

/* Flat button - link-style action */
.forgot-password .e-btn {
  --bs-primary: #6c757d;
  background: transparent;
  border: none;
  text-decoration: underline;
  font-size: 14px;
}

/* Outline button - secondary action */
.sign-up .e-btn {
  --bs-primary: #6c757d;
  border: 1px solid #6c757d;
}
```
**Native HTML Check:** If generated code uses a native HTML element (e.g., `<div>`, `<span>` for UI controls), verify a Syncfusion alternative exists in the component skills before using it. Replace with Syncfusion component if available.
---

### Reading Component Skills BEFORE Using generate code (MANDATORY)

**CRITICAL:** Do NOT assume component properties or APIs.

**Required Process:**
1. **Identify all mapped components** from Stage 3 output
   - E.g., GridComponent, ChartComponent, SidebarComponent, etc.
   - **MUST read getting-started for EVERY component in the Stage 3 list** - no exceptions

2. **For EACH component**, read the component skill:
   - Location: `{.agent-root}/skills/<component-skill>/references/getting-started.md`
   - Extract: imports, required props, setup code
   - Read: feature-specific guides (filtering, sorting, validation, styling, etc.)

3. **DO NOT generate code without reading** component skill documentation
   - Don't assume prop names or API structure
   - Don't guess at event handler names
   - Don't skip required setup or initialization

**Example - Reading GridComponent Skill:**
```
Before generating code:
1. Read: {.agent-root}/skills/syncfusion-angular-grid/references/getting-started.md
   → Extract: import { GridComponent } from '@syncfusion/ej2-angular-grids'
   → Read: required input properties, dataSource structure, column definitions

2. Read: {.agent-root}/skills/syncfusion-angular-grid/references/sorting.md
   → Understand: allowSorting property, sortSettings structure

3. Read: {.agent-root}/skills/syncfusion-angular-grid/references/filtering.md
   → Understand: allowFiltering property, filterSettings structure

4. NOW generate code with correct imports, properties, and API calls
```

**What Component Skills Contain:**
- ✅ Authoritative import statements
- ✅ Complete API documentation
- ✅ Feature-specific patterns (sorting, filtering, validation)
- ✅ Best practices and performance considerations
- ✅ Accessibility requirements
- ✅ Theme customization options

**Common Mistakes to Avoid:**
- ❌ Guessing prop names → Read skill documentation
- ❌ Missing style imports → Extract from syncfusion-themes.md
- ❌ Wrong event handler names → Copy from component skill examples
- ❌ Incomplete setup code → Follow skill's recommended initialization

---

**Component Structure for Complex UIs:**

For UIs with multiple distinct sections of a webpage (e.g., Header, Sidebar, Main Content, Footer), split into separate component files per webpage section. Each section gets its own folder with its .ts, .html, .css. **Each section folder MUST implement the appropriate Syncfusion components for that section** — do not mix section responsibilities. Create a parent component that composes these section components. Do not collapse multiple distinct UI sections into a single file.

**Example Output Files (Complex UI):**

```
components/
├── Header/
│   ├── header.component.ts       # Implement using Syncfusion AppBar
│   ├── header.component.html
│   └── header.component.css
├── Sidebar/
│   ├── sidebar.component.ts      # Implement using Syncfusion Sidebar/Menu
│   ├── sidebar.component.html
│   └── sidebar.component.css
├── MainContent/
│   ├── maincontent.component.ts  # Implement using Grid, Chart, Cards, etc.
│   ├── maincontent.component.html
│   └── maincontent.component.css
└── Footer/
    ├── footer.component.ts      # Implement navigation links, copyright
    ├── footer.component.html
    └── footer.component.css
```
---

## Component Integration & File Mapping

**Important:**
In a default Angular project, the app.html file contains placeholder template content.
The following content is only a sample template provided by Angular and can be safely replaced:
 
**"The content below is only a placeholder and can be replaced. Delete the template below to get started with your project!"**
 
If this default Angular template (including styles and main layout tags) is present in your application, you should remove it to properly display your custom UI on the page.

**Generated files MUST be wired to display in the app:**

1. **Import in App Component**:
   ```typescript
   import { Component } from '@angular/core';
   import { HeaderComponent } from './components/Header/header.component';
   import { SidebarComponent } from './components/Sidebar/sidebar.component';
   import { MainContentComponent } from './components/MainContent/maincontent.component';
   import { FooterComponent } from './components/Footer/footer.component';
   
   @Component({
     selector: 'app-root',
     template: `
       <app-header></app-header>
       <app-sidebar></app-sidebar>
       <app-maincontent></app-maincontent>
       <app-footer></app-footer>
     `,
     standalone: true,
     imports: [HeaderComponent, SidebarComponent, MainContentComponent, FooterComponent]
   })
   export class AppComponent {}
   ```

3. **Ensure CSS is loaded**:
   - If no framework/greenfield CSS styles: Automatically imported in component
   - If Tailwind: Classes applied directly
   - If Syncfusion theme: Already imported at app entry point (Stage 4)

**Without this mapping, component won't render in sample.**
**Without proper app.html cleanup when using routing, both the placeholder AND routed component will render, causing duplicate content.**

## Syncfusion component and theme Package Installation

**CRITICAL:** After code generation completes, you MUST install all Syncfusion component and theme packages that were used in the generated code. Run the appropriate `npm install` command for each package identified during the component skill reading phase (Stage 5, Steps 1-3).

Example:
```bash
npm install @syncfusion/ej2-angular-grids @syncfusion/ej2-angular-charts @syncfusion/ej2-angular-buttons @syncfusion/ej2-tailwind3-theme
```

**Without installing these packages, the generated code will fail to render.**

**User Interaction:** 
Optional review of generated code. No blocking confirmation.

**Status:** AI generates without user decision. User can review/adjust if needed.
