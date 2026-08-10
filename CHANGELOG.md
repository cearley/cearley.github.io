# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.5] - 2026-08-09

### Changed
- Homepage hero headline refined from "Senior Engineering" to "Software Engineering. One Engagement at a Time." for clarity — the previous phrase read ambiguously and isn't a standalone construction in common usage
- Seniority positioning ("30+ years") moved into the "From Concept to Code" intro section instead of the headline
- Hero H1 font-size retuned so the new headline still wraps to 2 lines

## [1.0.4] - 2026-08-08

### Added
- Open Graph share image and favicon regenerated to match the site's current brand palette
- New brand photography for the homepage hero, "From Concept to Code" thumbnail, and About page banner, replacing the theme's generic stock photos
- Sourced photo library (`static/images/brand/sourced/`) with license credits, for future site imagery

### Changed
- Homepage color palette retuned to a muted steel-indigo family to match the new hero photo
- Homepage and About page copy rewritten to reflect actual positioning and engagement model, replacing generic theme placeholder text
- About, Privacy Policy, Terms of Use, and Contact pages rewritten in a consistent company voice (previously a mix of first-person and company voice)

### Fixed
- Homepage hero headline corrected to avoid implying on-demand/always-available staffing; years of experience corrected from 20+ to 30+
- `terms.md` content-ownership clause corrected — site photography is licensed Unsplash stock, not original work
- Excessive whitespace and oversized/black page-title styling on About, Privacy Policy, and Terms of Use headers
- Backend: bumped transitive `serialize-javascript` dependency (via `mocha`) to 7.1.0, resolving one high and one moderate severity advisory

## [1.0.3] - 2026-08-07

### Removed
- Removed theme demo content from `posts`, `work`, and `portfolio` sections (unfilled Hugo Advance scaffold placeholders)
- Removed demo service pages (branding, user experience, web design, web development)

### Added
- Archetypes for `portfolio` and `services` content types to preserve front matter schema for future content

## [1.0.2] - 2026-01-23

### Changed
- Enabled social media footer links (LinkedIn, GitHub)
- Enabled blog and work sections on homepage (will display when content is added)
- Cleaned up homepage outro section (removed theme placeholder content)

### Removed
- Removed placeholder partner logos from `data/partners.json`
- Deleted unused `static/404.md` (Jekyll leftover; theme provides proper 404 page)
- Removed committed `.DS_Store` file from static directory

## [1.0.1] - 2026-01-22

### Added
- GitHub Actions workflow to automatically create releases from tags with changelog notes
- Version meta tag in HTML head showing deployed version (via theme update)

### Changed
- GitHub Pages deployment now triggers on release publish instead of push to main
- Added manual workflow dispatch with ref input to deploy any tag, branch, or SHA

## [1.0.0] - 2026-01-22

### Added
- Hugo Modules integration for private content (`private-content` repository)
- Hugo Modules integration for theme (`private-hugo-theme` repository)
- AWS SAM serverless backend with Lambda and API Gateway
- GitHub Actions workflow for Hugo deployment
- GitHub Actions workflow for CodeQL security analysis
- Apache 2.0 license with NOTICE file
- Documentation: README.md, CLAUDE.md, docs/PRIVATE-CONTENT.md

### Changed
- Theme now imported via Hugo Modules (previously vendored in `themes/`)
- Content structure supports mounting from private repositories

[Unreleased]: https://github.com/cearley/cearley.github.io/compare/v1.0.5...HEAD
[1.0.5]: https://github.com/cearley/cearley.github.io/compare/v1.0.4...v1.0.5
[1.0.4]: https://github.com/cearley/cearley.github.io/compare/v1.0.3...v1.0.4
[1.0.3]: https://github.com/cearley/cearley.github.io/compare/v1.0.2...v1.0.3
[1.0.2]: https://github.com/cearley/cearley.github.io/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/cearley/cearley.github.io/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/cearley/cearley.github.io/releases/tag/v1.0.0
