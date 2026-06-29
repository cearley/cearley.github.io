## ADDED Requirements

### Requirement: Hugo Module Initialization

The project SHALL be initialized as a Hugo Module to enable importing content and themes from external repositories.

#### Scenario: Module initialization creates go.mod

- **WHEN** running `hugo mod init github.com/cearley/cearley.github.io`
- **THEN** a `go.mod` file is created in the project root
- **AND** the module path is set to `github.com/cearley/cearley.github.io`

### Requirement: Private Theme Import

The Hugo Advance theme SHALL be imported from a private repository via Hugo Modules, removing licensed theme files from the public repository.

#### Scenario: Theme mounted from private repository

- **WHEN** Hugo builds the site
- **THEN** the theme is fetched from `github.com/cearley/private-content`
- **AND** mounted to `themes/hugo-advance`
- **AND** no theme files exist in the public repository's `themes/` directory

#### Scenario: Local development with private module

- **WHEN** a developer runs `hugo server` locally
- **THEN** the private module is accessible via SSH or HTTPS credentials
- **AND** the site builds and serves correctly

### Requirement: CI/CD Private Module Authentication

GitHub Actions SHALL authenticate to private repositories using a Personal Access Token to fetch Hugo Modules during build.

#### Scenario: GitHub Actions builds with private module

- **WHEN** the GitHub Actions workflow runs
- **THEN** Go is installed for Hugo Module support
- **AND** git is configured to use the `PRIVATE_REPO_PAT` secret for authentication
- **AND** `GOPRIVATE` is set to `github.com/cearley/*`
- **AND** the Hugo build completes successfully

#### Scenario: Missing PAT causes build failure

- **WHEN** the `PRIVATE_REPO_PAT` secret is not configured
- **THEN** the Hugo build fails with an authentication error
- **AND** an error message indicates the private module cannot be accessed

### Requirement: License Compliance

Licensed theme files SHALL NOT be present in any public repository to comply with the Zerostatic Pro License terms.

#### Scenario: Public repository contains no theme files

- **WHEN** cloning the public repository fresh
- **THEN** the `themes/hugo-advance/` directory does not exist
- **AND** no Zerostatic/Hugo Advance theme files are present anywhere in the repository
