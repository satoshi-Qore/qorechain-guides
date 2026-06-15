# Documentation Standards

This page defines basic documentation standards for QoreChain Guides.

The goal is to keep community-maintained pages clear, bilingual, practical, and safe to use before and after mainnet updates.

## Core Principles

| Principle | Guidance |
|---|---|
| Neutral tone | Avoid promotional or unsupported claims |
| Source awareness | Point users to official sources for critical or changing details |
| Bilingual alignment | Keep Turkish and English pages structurally similar when possible |
| Practical format | Prefer checklists, tables, and short explanations |
| Safety first | Do not publish private keys, seeds, credentials, or personal infrastructure details |

## Page Structure

Recommended structure for new guide pages:

```text
# Page Title

Short description of what the page explains.

## Scope

What this page covers and what it does not cover.

## Checklist or Steps

Short, verifiable actions.

## Common Notes

Important reminders, risks, or limitations.

## Related Resources

Links to related pages.

## Disclaimer

Community-maintained note and official-source reminder.
```

## Language Guidelines

### English

- Use short sentences.
- Avoid unnecessary jargon.
- Define technical terms when first used.
- Use placeholders such as `YOUR_RPC_URL`, `YOUR_SERVER_IP`, and `YOUR_CHAIN_ID`.

### Turkce

- Cumleleri kisa ve uygulanabilir tutun.
- Teknik terimleri ilk kullanildiginda açıklayın.
- Gerektiginde Ingilizce terimi parantez icinde verin.
- Orneklerde `YOUR_RPC_URL`, `YOUR_SERVER_IP`, `YOUR_CHAIN_ID` gibi placeholder kullanin.

## Mainnet-Sensitive Content

Some topics may change after official mainnet announcements or deployment.

Use cautious wording for:

- Rewards
- Commissions
- Validator requirements
- Staking rules
- Tokenomics details
- Governance parameters
- RPC endpoints
- Chain IDs

Recommended wording:

```text
This should be verified against official QoreChain documentation and current announcements.
```

Avoid wording such as:

```text
This will always work.
Rewards are guaranteed.
This is the final mainnet configuration.
```

## File Naming

Use clear lowercase names with hyphens.

Examples:

```text
en/glossary.md
tr/terimler-sozlugu.md
en/knowledge-base.md
tr/bilgi-bankasi.md
```

## Link Rules

- Prefer relative links for pages inside this repository.
- Use official links for critical external references.
- Avoid linking to unverified community claims as primary evidence.
- Check links after renaming files.

## Review Checklist

Before publishing a page, check:

- Does the page avoid unsupported claims?
- Are placeholders used instead of private data?
- Are critical details marked as subject to official updates?
- Is the page easy for a beginner to scan?
- Is there a matching Turkish or English page planned?

## Disclaimer

This standard is for community documentation quality. It does not replace official QoreChain documentation, technical specifications, or announcements.
