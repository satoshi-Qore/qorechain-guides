# Pull Request Template — Contributor Reference

> **Note:** When you open a Pull Request on GitHub, the template in [`.github/pull_request_template.md`](../.github/pull_request_template.md) is loaded automatically into the PR description field. That template is bilingual (Turkish/English) and tailored for documentation contributions to this repository.
>
> This file is a supplementary reference for contributors who want to review the PR checklist before opening a PR.

---

## What the GitHub PR Template Covers

When opening a PR, GitHub will pre-fill the description with a template that asks for:

- **Summary / Özet** — Brief description of the PR purpose
- **Change type / Değişiklik türü** — New content, correction, translation, troubleshooting, or other
- **Affected pages / Etkilenen sayfalar** — Files changed or added
- **Language / Dil** — Turkish, English, or both
- **Checklist / Kontrol listesi** — Links work, commands are in correct context, Turkish and English pages are structurally aligned, official sources referenced where needed

---

## Pre-PR Checklist

Before submitting a PR, confirm:

- [ ] All internal links have been checked and resolve correctly
- [ ] Commands are verified and placed in correct context
- [ ] Turkish and English pages remain structurally aligned where applicable
- [ ] No private keys, credentials, API keys, or sensitive infrastructure details are included
- [ ] Mainnet-sensitive content (rewards, RPC endpoints, staking rules) references official sources
- [ ] New pages are added to [`docs/content-map.md`](../docs/content-map.md)
- [ ] New pages have a matching Turkish or English counterpart planned or noted in [`docs/translation-status.md`](../docs/translation-status.md)

---

## Related Resources

- [Contributing Guide](../CONTRIBUTING.md)
- [Style Guide](../STYLE_GUIDE.md)
- [Documentation Standards — Format](./documentation-standards.md)
- [Documentation Standards — Content](../docs/documentation-standards.md)
- [First Contribution Guide](./first-contribution.md)
