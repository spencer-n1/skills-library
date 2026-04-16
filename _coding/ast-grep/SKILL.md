---
name: ast-grep
description: Structural code search and replace using the ast-grep CLI. Find patterns by AST structure with metavariables, relational queries, and multi-language support.
type: utility
keywords: ["ast-grep", "structural search", "AST", "metavariables", "code patterns"]
auto_detect: false
agent_type: sub
---

# ast-grep

**Use when explicitly asked** — structural code search for complex patterns.

---

## Prerequisites

```bash
# macOS
brew install ast-grep

# npm
npm install -g @ast-grep/cli

# cargo
cargo install ast-grep
```

Verify: `ast-grep --version`

---

## Core Concepts

### Metavariables
Use `$NAME` to match any syntax node:

| Pattern | Matches |
|---------|---------|
| `$FUNC($ARGS)` | Any function call with any args |
| `await $EXPR` | Any awaited expression |
| `$VAR = $VALUE` | Any assignment |
| `function $NAME($PARAMS) { $BODY }` | Any function declaration |

### Relational Queries
Find code in specific contexts:

```yaml
# Find console.log inside functions
rule:
  pattern: console.log($MSG)
  inside:
    kind: function_declaration
```

```yaml
# Find async functions without try-catch
rule:
  kind: function_declaration
  pattern: async function $NAME($PARAMS) { $BODY }
  not:
    inside:
      pattern: try { $BODY } catch($E) { $CATCH }
```

---

## Quick Commands

### Simple Pattern Search
```bash
# Find all console.log calls
ast-grep run --pattern 'console.log($MSG)' --lang javascript .

# Find all await expressions
ast-grep run --pattern 'await $EXPR' --lang typescript .

# Find specific function calls
ast-grep run --pattern 'fetch($URL, $OPTS)' --lang javascript .
```

### Rule-Based Scan
```bash
# Run a YAML rule file
ast-grep scan --rule rule.yml .

# Run inline rules
ast-grep scan --inline-rules "id: my-rule
language: javascript
rule:
  pattern: console.log($ARG)" .
```

---

## Rule File Format (YAML)

```yaml
id: rule-name              # Required: unique identifier
language: javascript       # Required: see language list below
message: "Found $MATCH"    # Optional: message for matches
severity: warning          # Optional: hint, info, warning, error
rule:
  # Pattern matching
  pattern: $FUNC($ARGS)
  
  # Or kind matching
  kind: function_declaration
  
  # Relational constraints
  inside:
    kind: class_declaration
  
  has:
    field: body
    pattern: return $EXPR
  
  # Negation
  not:
    pattern: async function $NAME($PARAMS) { $BODY }
  
  # Composite logic
  all:
    - pattern: function $NAME($PARAMS) { $BODY }
    - has:
        pattern: await $EXPR
  
  any:
    - pattern: console.log($A)
    - pattern: console.error($A)

# Rewrite (optional)
fix: |
  console.debug($ARGS)

# Metadata
metadata:
  description: "Finds synchronous functions with await"
```

---

## Supported Languages

| Language | Code |
|----------|------|
| Bash/Shell | bash |
| C | c |
| C++ | cpp |
| C# | cs |
| CSS | css |
| Dart | dart |
| Go | go |
| HTML | html |
| Java | java |
| JavaScript | javascript |
| JSON | json |
| Kotlin | kotlin |
| Lua | lua |
| PHP | php |
| Python | python |
| Ruby | ruby |
| Rust | rust |
| Scala | scala |
| Swift | swift |
| TypeScript | typescript |
| YAML | yaml |

---

## Common Patterns

### Find async functions without error handling
```yaml
id: async-without-try-catch
language: typescript
rule:
  kind: function_declaration
  pattern: async function $NAME($PARAMS) { $BODY }
  not:
    has:
      kind: try_statement
```

### Find functions with too many parameters
```yaml
id: too-many-params
language: javascript
rule:
  kind: function_declaration
  has:
    field: parameters
    has:
      kind: identifier
    min: 4
```

### Find deprecated function usage
```yaml
id: deprecated-fetch
language: javascript
rule:
  pattern: oldFetch($URL)
fix: |
  newFetch($URL)
```

### Find React hooks in wrong place
```yaml
id: hook-in-loop
language: typescript
rule:
  pattern: useState($INIT)
  inside:
    kind: for_statement
```

### Find unused variables (simple)
```yaml
id: potentially-unused
language: javascript
rule:
  kind: variable_declarator
  pattern: $NAME = $VALUE
  not:
    followedBy:
      pattern: $NAME
```

---

## Workflow

When user asks for structural search:

1. **Understand the pattern** — what code structure are they looking for?
2. **Choose approach** — simple `--pattern` or full YAML rule?
3. **Draft the rule** — write pattern with metavariables
4. **Test on example** — verify the pattern matches what they want
5. **Run on codebase** — execute search
6. **Present results** — file paths, line numbers, context

---

## Integration Examples

### With CRM Diagnostics
If asked to "find where calls aren't being validated":

```bash
# Find save functions without validation
ast-grep scan --inline-rules "id: save-without-validation
language: python
rule:
  pattern: def save($PARAMS): $BODY
  not:
    has:
      pattern: validate($ARGS)" .
```

### Security Audit
```bash
# Find potential SQL injection
ast-grep run --pattern 'query($SQL)' --lang python .

# Find eval usage
ast-grep run --pattern 'eval($CODE)' --lang javascript .
```

---

## Options Reference

| Flag | Description |
|------|-------------|
| `--pattern '<pattern>'` | Inline pattern search |
| `--lang <language>` | Specify language |
| `--rule <file>` | Use YAML rule file |
| `--inline-rules "..."` | Inline YAML rule |
| `--rewrite '<replacement>'` | Replace matches |
| `--interactive` | Confirm each replacement |
| `--json` | Output as JSON |
| `--threads <n>` | Parallel threads |
| `--filter <path>` | Only search specific paths |

---

## Testing Rules

Before running on full codebase, test on a small example:

```bash
# Create test file
echo "function test() { console.log('hi'); }" > /tmp/test.js

# Test pattern
ast-grep run --pattern 'console.log($X)' --lang javascript /tmp/test.js

# Should match? Verify before full run
```

---

## Output Formats

**Default (human-readable):**
```
src/app.ts:42
42│    console.log("debug")
```

**JSON (`--json`):**
```json
{
  "file": "src/app.ts",
  "line": 42,
  "column": 5,
  "text": "console.log",
  "metaVariables": { "$MSG": "\"debug\"" }
}
```

---

## Resources

- [ast-grep docs](https://ast-grep.github.io/)
- [Playground](https://ast-grep.github.io/playground.html) — test patterns online
- [Rule reference](https://ast-grep.github.io/reference/rule.html)
