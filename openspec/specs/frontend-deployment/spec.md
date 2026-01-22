# Frontend Deployment

## Purpose

The site frontend is automatically deployed to GitHub Pages via GitHub Actions on push to the main branch.

## Requirements

### Requirement: GitHub Actions CI/CD

The site SHALL automatically build and deploy to GitHub Pages when changes are pushed to the `main` branch.

#### Scenario: Automatic deployment on push

- **WHEN** commits are pushed to the `main` branch
- **THEN** the GitHub Actions workflow `hugo.yaml` triggers
- **AND** Hugo builds the site
- **AND** the built site is deployed to GitHub Pages

#### Scenario: Hugo version consistency

- **WHEN** the GitHub Actions workflow runs
- **THEN** it uses Hugo version 0.154.0
- **AND** the build matches local development builds

### Requirement: Custom Domain Configuration

The site SHALL be served from the custom domain `craigearley.software`.

#### Scenario: Custom domain routing

- **WHEN** users visit `craigearley.software`
- **THEN** GitHub Pages serves the site content
- **AND** the domain is configured via the `static/CNAME` file

### Requirement: Security Analysis

The site SHALL run CodeQL security analysis via GitHub Actions.

#### Scenario: Security scanning

- **WHEN** code changes are pushed
- **THEN** the `codeql.yaml` workflow runs security analysis
- **AND** vulnerabilities are reported in GitHub Security tab
