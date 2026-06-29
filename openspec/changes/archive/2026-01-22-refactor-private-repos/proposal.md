# Change: Separate Hugo Theme from Private Content Repository

## Why

The current `private-content` repository conflates infrastructure (the licensed Hugo theme) with content (articles, portfolio, resume). This creates friction for the content hub architecture where content is frequently updated and shared across multiple publishing targets, while the theme is stable infrastructure.

## What Changes

- **Rename** `github.com/cearley/private-content` → `github.com/cearley/private-hugo-theme`
- **Create** new `github.com/cearley/private-content` repository for actual content
- **Update** Hugo module import path in `config.toml`
- **Update** `go.mod` dependency
- **Move** `LICENSE` (Zerostatic Pro) to `private-hugo-theme` with the theme
- **Update** `PRIVATE_REPO_PAT` scope to include the renamed repo

## Impact

- Affected specs: `hugo-modules`
- Affected code: `config.toml`, `go.mod`, `.github/workflows/hugo.yaml` (PAT scope)
- Affected repos: `private-content` (renamed), new `private-content` (created)

## Benefits

- Clean separation: infrastructure (theme) vs content
- Content hub can evolve independently of theme
- Theme repository stable, rarely touched
- Matches architecture in `docs/PRIVATE-CONTENT.md`
