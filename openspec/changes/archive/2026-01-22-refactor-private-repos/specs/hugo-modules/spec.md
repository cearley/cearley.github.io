## MODIFIED Requirements

### Requirement: Private Theme Import

The Hugo Advance theme SHALL be imported from a dedicated private theme repository via Hugo Modules, separating infrastructure from content.

#### Scenario: Theme mounted from private theme repository

- **WHEN** Hugo builds the site
- **THEN** the theme is fetched from `github.com/cearley/private-hugo-theme`
- **AND** mounted to `themes/hugo-advance`
- **AND** no theme files exist in the public repository's `themes/` directory

#### Scenario: Local development with private theme module

- **WHEN** a developer runs `hugo server` locally
- **THEN** the private theme module is accessible via SSH or HTTPS credentials
- **AND** the site builds and serves correctly

### Requirement: CI/CD Private Module Authentication

GitHub Actions SHALL authenticate to private repositories using a Personal Access Token to fetch Hugo Modules during build.

#### Scenario: GitHub Actions builds with private theme module

- **WHEN** the GitHub Actions workflow runs
- **THEN** Go is installed for Hugo Module support
- **AND** git is configured to use the `PRIVATE_REPO_PAT` secret for authentication
- **AND** `GOPRIVATE` is set to `github.com/cearley/*`
- **AND** the Hugo build completes successfully fetching from `private-hugo-theme`

#### Scenario: Missing PAT causes build failure

- **WHEN** the `PRIVATE_REPO_PAT` secret is not configured
- **THEN** the Hugo build fails with an authentication error
- **AND** an error message indicates the private module cannot be accessed

## ADDED Requirements

### Requirement: Separate Content Repository

A dedicated private content repository SHALL exist for articles, portfolio, resume, and notes content, separate from the theme infrastructure.

#### Scenario: Content hub repository initialized

- **WHEN** the content hub is set up
- **THEN** `github.com/cearley/private-content` exists as a private repository
- **AND** it contains directories for `articles/`, `portfolio/`, `resume/`, and `notes/`
- **AND** it is initialized as a Go module for Hugo Module imports

#### Scenario: Future content imports from content hub

- **WHEN** content is added to the private-content repository
- **THEN** it can be mounted into the Hugo site via additional module imports
- **AND** the theme and content remain in separate repositories

### Requirement: License Compliance

The Zerostatic Pro License file SHALL reside with the theme in the private theme repository.

#### Scenario: License travels with theme

- **WHEN** examining the `private-hugo-theme` repository
- **THEN** the LICENSE file is present at the repository root
- **AND** the public repository does not contain the Zerostatic Pro License
