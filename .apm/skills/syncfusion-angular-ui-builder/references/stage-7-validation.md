# Stage 7: Validation

**Purpose:** Validate generated code against web standards. Binary pass/fail result.

**AI Should:**

1. **Validate WCAG 2.1 AA Compliance:**
   - Semantic HTML structure used? (form, label, input, button tags)
   - ARIA labels on form fields?
   - Keyboard navigation supported? (tab order, focus management)
   - Color contrast ≥ 4.5:1 for text?
   - Focus indicator visible on interactive elements?

2. **Check Security:**
   - No XSS vulnerabilities (DomSanitizer used for dynamic content)
   - No hardcoded secrets/API keys
   - Input sanitized if needed
   - Event bindings use proper Angular syntax

3. **Verify Performance:**
   - OnPush change detection strategy used?
   - No unnecessary change detection cycles?
   - Lazy loading where applicable?
   - Code is optimized?

4. **Check Responsive Design:**
   - Mobile-first approach (320px+)
   - Flexbox/Grid used for layouts?
   - Media queries for breakpoints?
   - Touch targets ≥ 44x44px?

**Validation Result:**

Binary: **PASS ✓** or **FAIL ✗**

**If PASS:**
```
✓ Validation Result: PASS

All standards met:
  ✓ WCAG 2.1 AA accessibility
  ✓ Security checks
  ✓ Performance standards
  ✓ Responsive design
  ✓ Code quality

Ready to proceed to dependencies...
```

**If FAIL:**
```
✗ Validation Result: FAIL

Issues found:
  ✗ Color contrast on label text (3.2:1, need 4.5:1)
  ✗ Form inputs missing aria-describedby attributes

Auto-fixes applied:
  ✓ Increased font size for contrast
  ✓ Added aria-describedby to inputs

Remaining issues: 0
Result: PASS (after fixes)
```

**If FAIL (with remaining issues):**
```
✗ Validation Result: FAIL

Issues found:
  ✗ Form requires aria-live region for errors
  ✗ Need custom input styling

Auto-fixes applied:
  ✓ Added aria-live region to form
  ✓ Added base input styling

Remaining issues: 0
Result: PASS (after fixes)
```

**User Interaction:**

If result is PASS: Proceed to next stage - NO Confirmation needed.

If result is FAIL (unresolvable issues):
```
Validation failed with 2 issues (not auto-fixable):
  - Custom form styling conflicts with Syncfusion theme
  - Animation timing needs adjustment for performance

Override and proceed anyway?
[Override & Proceed] [Request Manual Fixes] [Stop]
```

**Status:** - User confirms validation result or overrides upon failures.

**Reference:** See web-standards.md for complete validation rules and correction methods.

---

## Validation Checklist for Angular Components

### WCAG 2.1 AA Compliance ✓
- ✅ Semantic HTML5 elements used (`<form>`, `<label>`, `<input>`, `<button>`, etc.)
- ✅ ARIA attributes on interactive elements (aria-label, aria-describedby, aria-invalid)
- ✅ Keyboard navigation working (Tab order, Enter/Space for buttons, arrow keys for menus)
- ✅ Focus management implemented (focus trap in modals, visible focus indicator)
- ✅ Color contrast ≥ 4.5:1 for text, ≥ 3:1 for large text/UI components
- ✅ Touch targets ≥ 44x44px minimum
- ✅ Form validation error messages associated with inputs

### Security ✓
- ✅ No XSS vulnerabilities (DomSanitizer used for dynamic HTML content)
- ✅ No hardcoded secrets or API keys
- ✅ Input validation and sanitization applied
- ✅ Angular event bindings (not inline event handlers)
- ✅ No direct DOM manipulation (`nativeElement` only when necessary)

### Performance ✓
- ✅ OnPush change detection strategy for optimal performance
- ✅ TrackBy function used in *ngFor loops
- ✅ No unnecessary subscriptions (unsubscribe on destroy)
- ✅ Lazy loading for large datasets/images
- ✅ Component memoization where applicable

### Responsive Design ✓
- ✅ Mobile-first approach (320px minimum width)
- ✅ Flexbox/CSS Grid for layouts (no fixed widths)
- ✅ Media queries at 768px, 1024px, 1280px+ breakpoints
- ✅ Touch-friendly spacing (8px minimum gap between interactive elements)
- ✅ Viewport meta tag present in index.html

### Code Quality ✓
- ✅ TypeScript strict mode enabled (no `any` types)
- ✅ Angular linting (ESLint + Angular-specific rules)
- ✅ Proper Angular component structure (@Component decorator, lifecycle hooks)
- ✅ Comments and JSDoc for complex logic
- ✅ CSS properly scoped (view encapsulation)

### Router Integration ✓ (when routing is used)
- ✅ `app.html` contains ONLY `<router-outlet />` (no placeholder content)
- ✅ Default Angular placeholder content removed