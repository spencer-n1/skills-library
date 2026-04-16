---
name: playwright-cli
description: Automate browser interactions using Playwright CLI for testing, screenshots, form filling, and element interaction.
type: utility
keywords: ["playwright", "browser automation", "test website", "screenshot", "click element", "fill form", "automate browser", "page snapshot"]
auto_detect: true
agent_type: main
input_schema:
  command: string (required)
  url: string (optional)
  target: string (optional) - element ref, CSS selector, or locator
  text: string (optional) - for type/fill commands
  session: string (optional) - session name (-s flag)
  options: object (optional) - additional flags
output_schema:
  result: stdout/stderr
  snapshot: YAML file (optional)
  screenshot: PNG file (optional)
  pdf: PDF file (optional)
quality_metrics:
  success_rate: 0.95
  avg_tokens: 800
evolution:
  parent: null
  version: "1.0"
  lineage: []
status: active
---

# Playwright CLI

**Version:** 1.0  
**Type:** Utility  
**Status:** Active

---

## Purpose

Automate browser interactions using Playwright CLI. Token-efficient browser automation that doesn't force page data into LLM context.

**Use this when:**
- Testing website flows and interactions
- Taking screenshots of pages or elements
- Filling forms and clicking buttons
- Extracting page structure via snapshots
- Debugging UI issues
- Automating repetitive browser tasks

**Don't use when:**
- You need complex JavaScript execution (use `eval` or `run-code` sparingly)
- The site blocks automation (check robots.txt, terms)
- You need persistent sessions across long workflows (use `--persistent` flag)

---

## Prerequisites

```bash
# Install globally
npm install -g @playwright/cli@latest

# Or use npx
npx --no-install playwright-cli --version
```

## Configuration

This skill uses a local config file to keep output contained within the skill folder:

```bash
# Set config path before running commands
$env:PLAYWRIGHT_MCP_CONFIG="skills/_coding/playwright-cli/playwright-cli.json"
```

Or on macOS/Linux:
```bash
export PLAYWRIGHT_MCP_CONFIG="skills/_coding/playwright-cli/playwright-cli.json"
```

---

## Input

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `command` | string | yes | CLI command (open, click, type, screenshot, etc.) |
| `url` | string | sometimes | Target URL |
| `target` | string | sometimes | Element ref (e34), CSS selector (#btn), or locator |
| `text` | string | sometimes | Text for type/fill commands |
| `session` | string | optional | Named session (-s flag) |
| `options` | object | optional | Additional flags (--headed, --filename, etc.) |

---

## Output

- **Command result:** stdout with snapshot summary or confirmation
- **Snapshot:** YAML file with page structure and element refs
- **Screenshot:** PNG file saved to workspace
- **PDF:** PDF file of the page

---

## Quick Reference

### Core Commands
```
open [url]              # Open browser, optionally navigate
goto <url>              # Navigate to URL
click <ref>             # Click element
type <text>             # Type text
fill <ref> <text>       # Fill input field
fill <ref> <text> --submit  # Fill and press Enter
hover <ref>             # Hover over element
select <ref> <val>      # Select dropdown option
check <ref>             # Check checkbox/radio
uncheck <ref>           # Uncheck checkbox/radio
drag <start> <end>      # Drag and drop
upload <file>           # Upload file(s)
press <key>             # Press keyboard key
snapshot                # Capture page snapshot
screenshot              # Take screenshot
pdf                     # Save page as PDF
close                   # Close browser
```

### Targeting Elements

Use **refs from snapshots** (recommended):
```bash
playwright-cli snapshot
playwright-cli click e15
```

Or CSS selectors:
```bash
playwright-cli click "#main > button.submit"
```

Or Playwright locators:
```bash
playwright-cli click "getByRole('button', { name: 'Submit' })"
```

### Sessions

```bash
playwright-cli -s=myapp open https://app.com --persistent
playwright-cli -s=myapp click e12
playwright-cli list                    # List all sessions
playwright-cli -s=myapp close          # Close specific session
```

### Common Patterns

**Screenshot a specific element:**
```bash
playwright-cli snapshot
playwright-cli screenshot e23 --filename=screenshots/button.png
```

**Test a form flow:**
```bash
playwright-cli open https://example.com/form
playwright-cli fill e5 "John Doe"
playwright-cli fill e6 "john@example.com"
playwright-cli click e8 --submit
playwright-cli snapshot
```

---

## Procedure

### Step 1: Verify Installation
Check if `playwright-cli` is available. If not, install it.

### Step 2: Build Command
Construct the command with:
- Base command
- Session flag if provided (`-s=sessionName`)
- Target URL if provided
- Options/flags as needed

### Step 3: Execute
Run via shell with appropriate timeout.

### Step 4: Parse Output
- Look for snapshot references (e1, e2, etc.)
- Identify saved files (screenshots, PDFs)
- Note any errors

### Step 5: Return Results
Provide:
- Command output summary
- Available element refs for next actions
- File paths for any generated outputs

---

## Failure Modes

| Issue | Response |
|-------|----------|
| Command not found | Install: `npm install -g @playwright/cli@latest` |
| Element not found | Run `snapshot` first to get valid refs |
| Timeout | Increase action timeout or check if page loaded |
| Session not found | Create session with `open` first |
| Screenshot fails | Ensure target element exists and is visible |

---

## Examples

**Example 1: Screenshot a website**
```bash
Input:  playwright-cli open https://example.com
        playwright-cli screenshot --filename=screenshots/home.png
Output: Screenshot saved to screenshots/home.png
```

**Example 2: Test a login flow**
```bash
Input:  playwright-cli open https://app.com/login
        playwright-cli fill e5 "user@example.com"
        playwright-cli fill e6 "password"
        playwright-cli click e8
        playwright-cli snapshot
Output: Snapshot showing logged-in state
```

**Example 3: Get element refs and click**
```bash
Input:  playwright-cli open https://example.com
        playwright-cli snapshot
        # Parse: e15 = "Sign Up" button
        playwright-cli click e15
        playwright-cli snapshot
Output: New snapshot after click
```

---

## Rules

- **Always snapshot first** when interacting with new pages
- **Use refs from snapshots** for reliability
- **Name sessions** for multi-step workflows
- **Save screenshots with --filename** for deliverables
- **Default to `screenshots/` folder** for organization
- **Close sessions** when done to free resources

---

## Integration

Use alongside:
- `_coding/ast-grep` for analyzing page source
- `_research/business-researcher` for auditing competitor sites
- `_prompts/prompt-builder` for creating redesign prompts from screenshots
