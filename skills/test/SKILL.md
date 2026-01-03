---
name: test
description: Execute AI-powered exploratory testing on web applications using natural language. Use when asked to test websites, verify user flows (login, checkout, forms), find accessibility issues, or run automated QA. Triggers on requests like "test this website", "check for accessibility issues", "verify the login flow works", or "find bugs on this page".
---

# ScoutQA Testing Skill

Use the `scoutqa` CLI to perform AI-powered exploratory testing on web applications.

## Running Tests

Executions typically take 2-10 minutes and produce verbose output (streaming agent reasoning, tool calls, screenshots). Run in background to continue other work:

```bash
scoutqa --url "https://example.com" --prompt "Your test instructions" > test-results.txt 2>&1 &
```

**Reading results efficiently:**

```bash
# Check last N lines for summary/errors
tail -n 50 test-results.txt

# Full results only when needed
cat test-results.txt
```

**Options:**

- `--url` (required): Website URL to test
- `--prompt` (required): Natural language testing instructions
- `--project-id` (optional): Associate with a project for tracking

## Writing Effective Prompts

Structure prompts with specific steps and expectations:

```bash
scoutqa --url "https://example.com" --prompt "
Test the user registration flow:
1. Navigate to signup page
2. Test form validation (empty fields, invalid email, weak password)
3. Submit with valid data
4. Verify confirmation step
5. Check for accessibility issues

Expected: Successful registration with proper error handling
"
```

Avoid vague prompts like "test the site" — be specific about what to test and verify.

## Presenting Results

After execution completes, extract and present to the user:

- **Execution ID** (e.g., `ex_abc123`) for reference
- **Browser URL** (e.g., `https://scoutqa.ai/t/ex_abc123`) for full interactive report with screenshots
- **Issues found** with severity and category (accessibility, usability, functional)

## Common Test Patterns

### Smoke Test

```bash
scoutqa --url "$URL" --prompt "
Smoke test: verify homepage loads, navigation works, login/logout functions,
critical user flows complete, no console errors
"
```

### Accessibility Audit

```bash
scoutqa --url "$URL" --prompt "
Accessibility audit: check WCAG 2.1 AA compliance, keyboard navigation,
screen reader compatibility, color contrast, form labels and ARIA attributes
"
```

### E-commerce Flow

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

### SaaS Application

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

## Following Up on Stuck Executions

If the remote agent gets stuck or needs clarification, use `send-message` to continue:

```bash
# Example: Agent is stuck at login, user provides credentials
scoutqa send-message --execution-id ex_abc123 --prompt "
Use these test credentials: username: testuser@example.com, password: TestPass123
"

# Example: Agent asks which flow to test next
scoutqa send-message --execution-id ex_abc123 --prompt "
Focus on the checkout flow next, skip the wishlist feature
"
```

## Troubleshooting

| Issue                        | Solution                                    |
| ---------------------------- | ------------------------------------------- |
| `command not found: scoutqa` | Install CLI: `npm i -g @scoutqa/cli@latest` |
| Auth expired / unauthorized  | Run `scoutqa auth login`                    |
