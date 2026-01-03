# ScoutQA for Claude Code

Run AI-powered exploratory tests on web applications using natural language prompts.

[ScoutQA](https://scoutqa.ai/) automatically tests your websites for accessibility issues, broken user flows, and usability problems — all from simple English instructions.

## Installation

1. Install the ScoutQA CLI:

```bash
npm i -g @scoutqa/cli@latest
```

2. Add your [API key][api-key] by logging in:

```bash
scoutqa auth login
```

3. Install the plugin:

```bash
claude plugin marketplace add https://github.com/scoutqa-dot-ai/claude-code
claude plugin i scoutqa-plugin@scoutqa-marketplace
```

## Upgrading

```bash
claude plugin marketplace update
```

## Usage

Ask Claude to test any website:

- "Test the login flow on https://example.com"
- "Check https://example.com for accessibility issues"
- "Run a smoke test on our staging site"
- "Verify the checkout process works"

## Development

```bash
claude --plugin-dir /path/to/repo
```

## Troubleshooting

Diagnostic tool for troubleshooting the installation and health of Claude Code and plugins:

```bash
claude doctor
```

Make sure you have the ScoutQA CLI installed:

```bash
scoutqa --version
```

Run Claude with verbose logging to see any plugin load errors:

```bash
claude --debug
```

Re-authenticate if your session expired:

```bash
scoutqa auth login
```
