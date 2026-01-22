# Web Site - Craig Earley Software, LLC

[![Deploy Hugo site](https://github.com/cearley/cearley.github.io/actions/workflows/hugo.yaml/badge.svg)](https://github.com/cearley/cearley.github.io/actions/workflows/hugo.yaml)
[![CodeQL](https://github.com/cearley/cearley.github.io/actions/workflows/codeql.yaml/badge.svg)](https://github.com/cearley/cearley.github.io/actions/workflows/codeql.yaml)

Personal portfolio website deployed at [craigearley.software](https://craigearley.software).

## Architecture

- **Frontend**: Hugo static site generator with Hugo Advance theme
- **Backend**: AWS SAM (Lambda + API Gateway)
- **Deployment**: GitHub Pages (frontend) + AWS (backend)

## Hugo Modules

This site uses [Hugo Modules](https://gohugo.io/hugo-modules/) to import content from private repositories:

| Module | Purpose |
|--------|---------|
| `private-hugo-theme` | Licensed Hugo Advance theme |
| `private-content` | Blog posts, portfolio, case studies |

See `docs/PRIVATE-CONTENT.md` for full documentation.

## Development

### Hugo Site

```bash
# Development server
hugo server

# Build static site
hugo
```

### Hugo Modules

```bash
# Update all modules (theme + content)
hugo mod get -u

# Show module dependency graph
hugo mod graph
```

### Backend (AWS SAM)

```bash
cd backend && sam build      # Build
cd backend && sam deploy     # Deploy
cd backend && sam local start-api  # Test locally
```

## Development Workflows

**Updating content (from private-content):**
1. Make changes in `github.com/cearley/private-content`
2. Push to private-content
3. In this repo: `hugo mod get -u`
4. Test: `hugo server`
5. Commit `go.mod` and `go.sum`, then push

**Updating site (config, layouts, static):**
1. Edit files directly
2. Test: `hugo server`
3. Commit and push
