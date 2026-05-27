# Stage 8 — Code Insertion

## Overview

Stage 5 generates all code files. Stage 6 installs all packages. This stage inserts files into the IDE in the correct order. The user accepts or rejects each diff.

---

## Pre-Check

Stop and state the reason if any check fails:

| Check | If Failed |
|-------|-----------|
| `component-mapping.json` fully resolved | Hard stop — missing components |
| All packages installed by Stage 6 | Hard stop — complete Stage 6 first |
| Overall Syncfusion theme CSS confirmed in Stage 6 output | Hard stop — theme missing |
| `app.component.ts` path is unambiguous | Ask user to confirm target file |

---

## Insertion Order

One file per response. Do not combine steps.

### Step 1 — Component Files

Insert sections in order: **Header → Sidebar → MainContent → Footer**

```
Creating: src/app/components/header/header.component.ts
Creating: src/app/components/header/header.component.html
Creating: src/app/components/header/header.component.css
```

CSS file immediately follows its component files. No placeholders. Complete code only.

For simple UIs (single component), insert that component set, then go to Step 2.

---

### Step 2 — app.component.ts Update

Show changed lines only — never the full file.

Updating: src/app/app.component.css
```ts

// 1. Overall Syncfusion theme import  (angular.json styles OR top-level styles.css)
@import '@syncfusion/ej2-[theme-package]/styles/[theme-name].css';
```
Updating: src/app/app.component.ts

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

---

### Step 3 — Build Verification

**Only run if Stage 7 validation was skipped.**
If Stage 7 ran and passed, skip this step — build is already verified.

```
All files inserted. Please run:

npm run build

Paste errors here if any — otherwise you're done.
```

---

## Rollback

- **VS Code / Cursor**: `Ctrl+Z` / `Cmd+Z`
- **Syncfusion Code Studio**: Undo in diff panel
- Or say *"undo the last file"* for regeneration

---

## Success Criteria

| Scenario | Criteria |
|----------|----------|
| Stage 7 ran | Files accepted + theme import in `app.component.ts` + layout accepted |
| Stage 7 skipped | Above + `ng build` passes |