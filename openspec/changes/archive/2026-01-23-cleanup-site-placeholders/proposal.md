# Change: Cleanup Site Placeholders and Quick Improvements

## Why

The site contains leftover placeholder content from the Hugo Advance theme that should be removed or customized. Additionally, there are several quick wins that would improve the site's professionalism and functionality.

## What Changes

### High Priority (Cleanup)

1. **Remove/Replace Placeholder Partner Data** - `data/partners.json` contains demo logos (Netflix, Slack, Algolia, etc.) linking to zerostatic.io (the theme vendor)
2. **Delete Unused 404.md File** - `static/404.md` is a leftover file (uses Jekyll syntax) that's not used by Hugo; the theme provides `layouts/404.html`
3. **Remove Theme Demo Content from Homepage** - `content/en/_index.md` has leftover "Buy Now" and "Save time and money using this premium Hugo theme" text in the outro section

### Medium Priority (Quick Wins)

4. **Enable Social Media Footer Links** - `data/social.json` has LinkedIn and GitHub configured, but `show_social_media_links = false` in config.toml
5. **Enable Blog Section on Homepage** - `blog.enabled = false` despite having blog content via private-content module
6. **Enable Work/Portfolio Section on Homepage** - `work.enabled = false` despite having case studies

### Low Priority (Optional Polish)

7. **Add Google Analytics** - `google_analytics_id = ""` is empty; add GA4 measurement ID if analytics are desired
8. **Remove .DS_Store from Repository** - `static/.DS_Store` is committed; should be in `.gitignore`

## Impact

### Affected Repositories

| Repository | Changes |
|------------|---------|
| **cearley.github.io** (main) | `data/partners.json`, `static/404.md`, `content/en/_index.md`, `config.toml`, `.gitignore` |
| **private-hugo-theme** | None required (404.html template is functional) |
| **private-content** | None required (content is separate from these configuration changes) |

**Note:** The `go.mod` has active `replace` directives pointing to local module directories. These changes only affect the main repository since they're data/config changes, not content or theme template changes.

### Affected Specs
- `site-theming` (data-driven content, static assets)

### Files to Modify
- `data/partners.json` - Remove or replace with real data
- `static/404.md` - Delete (unused)
- `content/en/_index.md` - Clean up or disable outro section
- `config.toml` - Enable social links, blog, work sections
- `.gitignore` - Add .DS_Store pattern
