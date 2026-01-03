# Common Test Patterns

Ready-to-use testing patterns for common scenarios. Copy and adapt these prompts for specific use cases.

## Smoke Test

Verify core functionality works after deployment:

```bash
scoutqa --url "$URL" --prompt "
Smoke test: verify homepage loads, navigation works, login/logout functions,
critical user flows complete, no console errors
"
```

## Accessibility Audit

Check WCAG compliance and assistive technology support:

```bash
scoutqa --url "$URL" --prompt "
Accessibility audit: check WCAG 2.1 AA compliance, keyboard navigation,
screen reader compatibility, color contrast, form labels and ARIA attributes
"
```

## E-commerce Flow

Test shopping experience from browse to checkout:

```bash
scoutqa --url "$URL" --prompt "
Test e-commerce flow:
1. Search and filter products
2. View product detail page with variants and pricing
3. Add to cart and verify persistence
4. Proceed through checkout steps
5. Verify cart quantity updates and pricing calculations
"
```

## SaaS Application

Test core application workflows:

```bash
scoutqa --url "$URL" --prompt "
Test SaaS application:
1. Login authentication flow
2. Dashboard widgets load with real data
3. CRUD operations on core entities
4. Settings and permissions enforcement
5. Search/filter across datasets
"
```

## Authentication Flow

Test login, registration, and password reset:

```bash
scoutqa --url "$URL" --prompt "
Test authentication:
1. Login with valid credentials
2. Login with invalid credentials (verify error handling)
3. Password reset flow
4. Session persistence after page refresh
5. Logout functionality
"
```

## Form Validation

Test input validation and error handling:

```bash
scoutqa --url "$URL" --prompt "
Test form validation:
1. Submit with empty required fields
2. Submit with invalid email format
3. Submit with weak password
4. Verify inline error messages appear
5. Verify successful submission with valid data
"
```

## Mobile Responsiveness

Test responsive design across viewports:

```bash
scoutqa --url "$URL" --prompt "
Test mobile responsiveness:
1. Navigation menu collapses to hamburger
2. Content reflows appropriately
3. Touch targets are adequately sized
4. No horizontal scrolling required
5. Images scale correctly
"
```
