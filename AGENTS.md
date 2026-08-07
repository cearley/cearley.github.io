<!-- OPENSPEC:START -->
# OpenSpec Instructions

These instructions are for AI assistants working in this project.

Always open `@/openspec/AGENTS.md` when the request:
- Mentions planning or proposals (words like proposal, spec, change, plan)
- Introduces new capabilities, breaking changes, architecture shifts, or big performance/security work
- Sounds ambiguous and you need the authoritative spec before coding

Use `@/openspec/AGENTS.md` to learn:
- How to create and apply change proposals
- Spec format and conventions
- Project structure and guidelines

Keep this managed block so 'openspec update' can refresh the instructions.

<!-- OPENSPEC:END -->

# AGENTS.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Hugo Modules

This site uses Hugo Modules to import content from private repositories:

| Module | Purpose | Mounts To |
|--------|---------|-----------|
| `private-hugo-theme` | Licensed Hugo Advance theme | Theme |
| `private-content` | Blog posts, portfolio, case studies | `content/en/posts`, `content/en/portfolio/github`, `content/en/work` |

See `docs/PRIVATE-CONTENT.md` for full documentation.

## Development Commands

See `backend/CLAUDE.md` for AWS SAM backend commands.

### Development Workflows

**Updating content (from private-content repo):**
1. Make changes in `github.com/cearley/private-content`
2. Commit and push to private-content
3. In this repo: `hugo mod get -u`
4. Test locally: `hugo server`
5. Commit updated `go.mod` and `go.sum`
6. Create a release to deploy (see Deployment section)

**Updating site (config, layouts, static files):**
1. Edit files directly in this repo
2. Test locally: `hugo server`
3. Commit and push
4. Create a release to deploy (see Deployment section)

**Local development with content changes:**

To develop with local copies of the private modules, add replace directives to `go.mod`:

```go
replace (
	github.com/cearley/private-content => /path/to/local/private-content
	github.com/cearley/private-hugo-theme => /path/to/local/private-hugo-theme
)
```

Then verify and start the development server:
```bash
hugo mod verify
hugo server
```

Changes to files in the local module directories will be reflected immediately.

**AI Agent Instructions:** When `replace` directives are present in `go.mod`, make content and theme changes in the local module directories specified by those paths:
- **Content changes** (blog posts, portfolio, case studies): Edit files in the `private-content` directory path
- **Theme changes** (layouts, partials, assets): Edit files in the `private-hugo-theme` directory path

Do not edit mounted content in this repository's `content/en/` directory when replace directives point to local modules.

**Important:** Remove the replace directives before committing. They contain absolute paths specific to your machine.

## Content Structure

### Main Content Directory (`content/`)

**Mounted from private-content (via Hugo Modules):**
- `posts/` - Blog articles (from `articles/*`)
- `portfolio/github/` - GitHub projects (from `portfolio/projects`)
- `work/` - Case studies (from `portfolio/case-studies`)

## Deployment

- **Frontend**: Deploys to GitHub Pages via GitHub Actions when a release is published
- **Backend**: Manual deployment via `sam deploy` command
- **Domain**: craigearley.software (configured in CNAME file)

See the `release` skill for the full release workflow (updating CHANGELOG.md, tagging, and deploying a specific version).