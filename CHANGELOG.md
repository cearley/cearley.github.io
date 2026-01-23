# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

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

[Unreleased]: https://github.com/cearley/cearley.github.io/compare/v1.0.2...HEAD
[1.0.2]: https://github.com/cearley/cearley.github.io/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/cearley/cearley.github.io/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/cearley/cearley.github.io/releases/tag/v1.0.0
