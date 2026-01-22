# Static Site Generation

## Purpose

The site is built using Hugo static site generator to produce a fast, secure, and easily deployable website from Markdown content.

## Requirements

### Requirement: Hugo Build Process

The site SHALL be built using Hugo static site generator version 0.154.0 to ensure consistent builds across local development and CI/CD.

#### Scenario: Local development server

- **WHEN** running `hugo server` in the project root
- **THEN** a local development server starts at `http://localhost:1313`
- **AND** live reload is enabled for content changes

#### Scenario: Production build

- **WHEN** running `hugo --environment production`
- **THEN** static files are generated in the `public/` directory
- **AND** assets are minified for production

### Requirement: Hugo Configuration

The site SHALL be configured via `config.toml` in the project root with all site-wide settings.

#### Scenario: Configuration file structure

- **WHEN** Hugo reads configuration
- **THEN** it loads settings from `config.toml`
- **AND** the base URL is set to `https://craigearley.software`

### Requirement: Multi-language Support Structure

The site SHALL support a multi-language directory structure with content organized under language-specific directories.

#### Scenario: English content directory

- **WHEN** content is created for the site
- **THEN** it is placed under `content/en/` directory
- **AND** Hugo serves it as the default language
