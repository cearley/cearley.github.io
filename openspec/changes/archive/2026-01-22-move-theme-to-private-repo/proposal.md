# Change: Move Hugo Advance Theme to Private Repository

## Why

The Hugo Advance theme was purchased under the Zerostatic Pro License, which explicitly prohibits redistribution:

> You can't re-distribute or re-sell this theme as stock, in a tool or template.

Having the theme in a public GitHub repository violates this license term. Moving it to a private content repository resolves this compliance issue while enabling a content hub architecture for future multi-target publishing.

## What Changes

- **BREAKING**: Remove `themes/hugo-advance/` directory from public repository
- Initialize Hugo Modules in the project (`go.mod`)
- Add module configuration to `config.toml` to import theme from private repo
- Update GitHub Actions workflow with Go setup and private module authentication
- Create `private-content` repository (if not exists) with theme files

## Impact

- Affected specs: `hugo-modules` (new capability)
- Affected code:
  - `config.toml` - Add `[module]` configuration
  - `.github/workflows/hugo.yaml` - Add Go setup, PAT authentication, GOPRIVATE
  - `themes/hugo-advance/` - Remove entirely from public repo
  - `go.mod`, `go.sum` - New files (auto-generated)
- External dependencies:
  - New private GitHub repository: `github.com/cearley/private-content`
  - GitHub Personal Access Token (fine-grained) for CI/CD
  - Go toolchain in CI (for Hugo Modules)
