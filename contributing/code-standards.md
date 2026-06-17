# Code Standards

All code contributions to QoreChain repositories must follow these standards.

## General

- Write code that is readable and easy to understand.
- Prefer clarity over cleverness.
- Keep functions short and focused on a single responsibility.
- Avoid unnecessary dependencies.

## Python

- Follow [PEP 8](https://peps.python.org/pep-0008/) for style.
- Use type hints for function signatures.
- Use dataclasses or named tuples for structured data.
- Handle exceptions explicitly -- avoid bare `except:`.
- Use `logging` instead of `print` for operational output.

```python
# Good
def check_endpoint(url: str, timeout: int = 10) -> CheckResult:
    ...

# Avoid
def check(x, t=10):
    ...
```

## Shell / Bash

- Use `#!/usr/bin/env bash` as the shebang.
- Set `set -euo pipefail` at the top of scripts.
- Quote all variable expansions: `"$VAR"`.
- Prefer `[[ ]]` over `[ ]` for conditionals.

## YAML

- Use 2-space indentation.
- Quote strings that contain special characters.
- Include comments for non-obvious fields.

## JSON

- Use 2-space indentation.
- Do not include trailing commas.
- Do not include comments.

## Commit Messages

All commit messages must be in English. Use the format:

```
type: short summary in present tense (max 72 chars)
```

Types: `fix`, `feat`, `docs`, `refactor`, `test`, `chore`

## Security

- Never commit credentials, API keys, tokens, or private endpoint URLs.
- Use placeholder values in example files.
- Do not log sensitive data.
