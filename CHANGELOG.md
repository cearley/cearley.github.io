# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

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

[Unreleased]: https://github.com/cearley/cearley.github.io/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/cearley/cearley.github.io/releases/tag/v1.0.0
