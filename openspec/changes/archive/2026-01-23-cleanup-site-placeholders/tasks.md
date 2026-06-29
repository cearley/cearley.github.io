# Tasks

## 1. High Priority - Cleanup Placeholder Content

- [x] 1.1 Remove or replace `data/partners.json` with real technology/partner logos, or delete if not needed
- [x] 1.2 Delete `static/404.md` (unused leftover file; theme provides `layouts/404.html`)
- [x] 1.3 Clean up `content/en/_index.md` outro section (remove zerostatic.io references and "Buy Now" text)

## 2. Medium Priority - Enable Existing Features

- [x] 2.1 Enable social media footer links in `config.toml` (`show_social_media_links = true`)
- [x] 2.2 Enable blog section on homepage in `content/en/_index.md` (`blog.enabled = true`)
- [x] 2.3 Enable work/portfolio section on homepage (`work.enabled = true`)
- [x] 2.4 Test homepage layout with newly enabled sections

## 3. Low Priority - Optional Polish

- [ ] 3.1 (Optional) Add Google Analytics ID to `config.toml` if analytics tracking is desired
- [x] 3.2 (Optional) Add `.DS_Store` to `.gitignore` and remove `static/.DS_Store` from repository

## 4. Verification

- [x] 4.1 Run `hugo server` and verify all changes render correctly
- [x] 4.2 Check 404 page renders properly (theme provides layouts/404.html)
- [x] 4.3 Verify footer social links appear (LinkedIn and GitHub icons confirmed)
- [x] 4.4 Verify homepage sections display content (configured; will show when private-content has articles)
