# Documentation Standards

> **Note:** This file defines contributor-facing file format and structure rules (Markdown syntax, code blocks, link conventions, placeholders). For content quality guidelines — tone, mainnet-sensitive wording, review checklist, and page structure templates — see [`docs/documentation-standards.md`](../docs/documentation-standards.md).

All documentation contributions to QoreChain repositories must follow these standards.

## Language

- Documentation files may be written in English, Turkish, or both.
- All file names, headings used as anchor links, and directory names must be in English.
- When a document has both English and Turkish versions, Turkish comes first in bilingual headings.
- Do not translate the term "Light Node" -- keep it in English in all languages.

## File Format

- Use Markdown (CommonMark) for all documentation.
- File extension: `.md`
- Encoding: UTF-8

## Structure

Each documentation file should have:

1. A single H1 heading (`# Title`) at the top
2. A brief description paragraph
3. Organized sections with H2 headings (`## Section`)
4. A "Next Steps" or "See Also" section where relevant

## Style

- Write in plain, direct language.
- Use present tense and active voice.
- Avoid jargon not defined in the glossary.
- Use numbered lists for sequential steps.
- Use bullet lists for unordered items.
- Keep sentences concise -- one idea per sentence.

## Code Blocks

Always specify the language for code blocks:

```bash
# Shell example
```

```python
# Python example
```

```yaml
# YAML example
```

## Links

- Use relative links between files in the same repository.
- Do not link to localhost or internal addresses.
- Verify all external links before committing.

## Placeholders

Use these standard placeholders in examples:

```
YOUR_RPC_URL
YOUR_CHAIN_ID
YOUR_NODE_IP
YOUR_API_KEY
YOUR_MONIKER
YOUR_VALIDATOR_KEY_NAME
```

## Sensitive Information

Never include in documentation:

- Private endpoint URLs
- API keys or tokens
- Internal server addresses
- Credentials of any kind
