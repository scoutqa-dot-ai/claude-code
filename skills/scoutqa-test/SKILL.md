---
name: scoutqa-test
description: This skill should be used when the user asks to "test this website", "run exploratory testing", "check for accessibility issues", "verify the login flow works", "find bugs on this page", or requests automated QA testing. Triggers on web application testing scenarios including smoke tests, accessibility audits, e-commerce flows, and user flow validation using ScoutQA CLI.
---

# ScoutQA Testing Skill

Perform AI-powered exploratory testing on web applications using the `scoutqa` CLI.

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

After execution completes, extract and present:

- **Execution ID** (e.g., `ex_abc123`) for reference
- **Browser URL** (e.g., `https://scoutqa.ai/t/ex_abc123`) for full interactive report with screenshots
- **Issues found** with severity and category (accessibility, usability, functional)

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

## Additional Resources

### Reference Files

For ready-to-use testing patterns, consult:
- **`references/patterns.md`** - Common test patterns (smoke tests, accessibility audits, e-commerce flows, SaaS applications, authentication, form validation, mobile responsiveness)
