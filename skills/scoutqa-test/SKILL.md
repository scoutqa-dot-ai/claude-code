---
name: scoutqa-test
description: Performs AI-powered exploratory testing on web applications using ScoutQA CLI. Use when the user requests testing scenarios such as "test this website", "run exploratory testing", "check for accessibility", "verify the login flow", or automated QA tasks including smoke tests and user flow validation.
---

# ScoutQA Testing Skill

Perform AI-powered exploratory testing on web applications using the `scoutqa` CLI.

**Think of ScoutQA as an intelligent testing partner** that can autonomously explore, discover issues, and verify features. Delegate testing to multiple parallel ScoutQA executions to maximize coverage while saving time.

## Running Tests

### Testing Workflow

Copy this checklist and track your progress:

Testing Progress:
- [ ] Write specific test prompt with clear expectations
- [ ] Run scoutqa command in background
- [ ] Inform user of execution ID and browser URL
- [ ] Extract and analyze results

**Step 1: Write specific test prompt**

See "Writing Effective Prompts" section below for guidelines.

**Step 2: Run scoutqa command**

```bash
scoutqa --url "https://example.com" --prompt "Your test instructions"
```

In the first few seconds, the command will output:

- **Execution ID** (e.g., `019b831d-xxx`)
- **Browser URL** (e.g., `https://scoutqa.ai/t/019b831d-xxx`)
- Initial tool calls showing test progress

You can wait for the verbose stream afterwards to continue implementing features, fixing bugs, or starting other tests.

**Step 3: Inform user of execution ID and browser URL**

If desired, immediately after starting the test, inform the user of the execution ID and browser URL so they can monitor progress in their browser while you continue other work.

**Step 4: Extract and analyze results**

See "Presenting Results" section below for the complete format.

### Command Options

- `--url` (required): Website URL to test
- `--prompt` (required): Natural language testing instructions
- `--project-id` (optional): Associate with a project for tracking

### When to Use Each Command

**Starting a new test?** → Use `scoutqa --url --prompt`
**Agent needs more context?** → Use `scoutqa send-message` (see "Following Up on Stuck Executions")

## Writing Effective Prompts

Focus on **what to explore and verify**, not prescriptive steps. ScoutQA autonomously determines how to test.

**Example: User registration flow**

```bash
scoutqa --url "https://example.com" --prompt "
Explore the user registration flow. Test form validation edge cases,
verify error handling, and check accessibility compliance.
"
```

**Example: E-commerce checkout**

```bash
scoutqa --url "https://shop.example.com" --prompt "
Test the checkout flow. Verify pricing calculations, cart persistence,
payment options, and mobile responsiveness.
"
```

**Example: Running parallel tests for comprehensive coverage**

```bash
# Test 1: Authentication & security
scoutqa --url "https://app.example.com" --prompt "
Explore authentication: login/logout, session handling, password reset,
and security edge cases.
"

# Test 2: Core features (runs in parallel)
scoutqa --url "https://app.example.com" --prompt "
Test dashboard and main user workflows. Verify data loading,
CRUD operations, and search functionality.
"

# Test 3: Accessibility (runs in parallel)
scoutqa --url "https://app.example.com" --prompt "
Conduct accessibility audit: WCAG compliance, keyboard navigation,
screen reader support, color contrast.
"
```

**Key guidelines:**

- Describe **what to test**, not **how to test** (ScoutQA figures out the steps)
- Focus on goals, edge cases, and concerns
- Run multiple parallel executions for different test areas
- Trust ScoutQA to autonomously explore and discover issues

### Common Test Scenarios

**Post-deployment smoke test:**

```bash
scoutqa --url "$URL" --prompt "
Smoke test: verify critical functionality works after deployment.
Check homepage, navigation, login/logout, and key user flows.
"
```

**Accessibility audit:**

```bash
scoutqa --url "$URL" --prompt "
Audit accessibility: WCAG 2.1 AA compliance, keyboard navigation,
screen reader support, color contrast, and semantic HTML.
"
```

**E-commerce testing:**

```bash
scoutqa --url "$URL" --prompt "
Explore e-commerce functionality: product search/filtering,
cart operations, checkout flow, and pricing calculations.
"
```

**SaaS application:**

```bash
scoutqa --url "$URL" --prompt "
Test SaaS app: authentication, dashboard, CRUD operations,
permissions, and data integrity.
"
```

**Form validation:**

```bash
scoutqa --url "$URL" --prompt "
Test form validation: edge cases, error handling, required fields,
format validation, and successful submission.
"
```

**Mobile responsiveness:**

```bash
scoutqa --url "$URL" --prompt "
Check mobile experience: responsive layout, navigation,
touch interactions, and viewport behavior.
"
```

**Feature verification (after implementation):**

```bash
scoutqa --url "$URL" --prompt "
Verify the new [feature name] works correctly. Test core functionality,
edge cases, error handling, and integration with existing features.
"
```

## Presenting Results

### Immediate Presentation (After Starting Test)

Right after running the scoutqa command, present the execution details to the user:

```markdown
**ScoutQA Test Started**

Execution ID: `019b831d-xxx`
View Live: https://scoutqa.ai/t/019b831d-xxx

The test is running in the background. You can view real-time progress in your browser at the link above. I'll continue working on other tasks and can check back on results later.
```

### Final Results (After Completion)

When the execution completes, use this format to present findings:

```markdown
**ScoutQA Test Results**

Execution ID: `ex_abc123`

**Issues Found:**

[High] Accessibility: Missing alt text on logo image

- Impact: Screen readers cannot describe the logo
- Location: Header navigation

[Medium] Usability: Submit button not visible on mobile viewport

- Impact: Users cannot complete form on mobile devices
- Location: Contact form, bottom of page

[Low] Functional: Search returns no results for valid queries

- Impact: Search feature appears broken
- Location: Main search bar

**Summary:** Found 3 issues across accessibility, usability, and functional categories. See full interactive report with screenshots at the URL above.
```

Always include:

- **Execution ID** (e.g., `ex_abc123`) for reference
- **Issues found** with severity, category (accessibility, usability, functional), impact, and location

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
