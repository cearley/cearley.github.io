---
name: release
description: Use when cutting a release or deploying cearley.github.io — the site only deploys when a GitHub release is published (not on push to main). Covers updating CHANGELOG.md, tagging, and re-deploying a specific past version.
---

The site deploys only when a GitHub release is published (not on push to main).

**Creating a release:**
1. Update `CHANGELOG.md`:
   - Move entries from `[Unreleased]` to new version section
   - Set the release date
   - Update comparison links at the bottom
2. Commit: `git commit -m "docs: prepare release v1.x.x"`
3. Create and push tag:
   ```bash
   git tag v1.x.x
   git push origin main
   git push origin v1.x.x
   ```
4. GitHub Actions automatically:
   - Creates a release with notes extracted from CHANGELOG.md
   - Deploys the site to GitHub Pages

**Deploying a specific version:**
1. Go to Actions → "Deploy cearley.software site to Pages"
2. Click "Run workflow"
3. Enter the git ref (tag like `v1.0.0`, branch, or commit SHA)
4. Click "Run workflow"
