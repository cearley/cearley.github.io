# Site Theming - Spec Delta

## MODIFIED Requirements

### Requirement: Data-Driven Content

The site SHALL support data-driven content via JSON files in the `data/` directory. Data files SHALL contain real, production-ready content rather than theme placeholder data.

#### Scenario: Partner and social data

- **WHEN** rendering partner logos or social links
- **THEN** data is loaded from `data/partners.json` and `data/social.json`
- **AND** templates iterate over the data
- **AND** all URLs point to legitimate external sites (not theme vendor demos)

#### Scenario: Social media links in footer

- **WHEN** social media links are enabled in config
- **THEN** footer displays icons linked from `data/social.json`
- **AND** links open to actual social profiles

### Requirement: Static Assets

The site SHALL serve static assets from the `static/` directory including images and favicon. The `static/` directory SHALL NOT contain unused or legacy files.

#### Scenario: Static asset serving

- **WHEN** the site is built
- **THEN** contents of `static/` are copied to the output
- **AND** assets are accessible at their relative paths
- **AND** no legacy Jekyll files exist in the static directory

#### Scenario: 404 error page

- **WHEN** a user navigates to a non-existent page
- **THEN** Hugo serves a 404 error page using the theme's `layouts/404.html` template
- **AND** navigation links function correctly

## ADDED Requirements

### Requirement: Homepage Section Configuration

The site SHALL support enabling or disabling homepage sections (blog, work, services, contact) via frontmatter configuration in `content/en/_index.md`.

#### Scenario: Enabling blog section on homepage

- **WHEN** `blog.enabled = true` in homepage frontmatter
- **THEN** recent blog posts are displayed on the homepage
- **AND** a "view all" link appears if `show_view_all = true`

#### Scenario: Enabling work section on homepage

- **WHEN** `work.enabled = true` in homepage frontmatter
- **THEN** featured case studies are displayed on the homepage
- **AND** content is pulled from `content/en/work/`

#### Scenario: Disabling placeholder content

- **WHEN** a homepage section contains theme placeholder content
- **THEN** the section SHALL be disabled or customized with real content
- **AND** no references to theme vendor sites (zerostatic.io) remain
