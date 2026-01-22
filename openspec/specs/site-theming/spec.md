# Site Theming

## Purpose

The site uses the Hugo Advance theme with customization options for dark mode, colors, fonts, and layout.

## Requirements

### Requirement: Hugo Advance Theme

The site SHALL use the Hugo Advance theme imported via Hugo Modules from a private repository for license compliance.

#### Scenario: Theme loading via Hugo Modules

- **WHEN** Hugo builds the site
- **THEN** it fetches the theme from `github.com/cearley/private-hugo-theme`
- **AND** mounts it to `themes/hugo-advance`
- **AND** applies theme templates and assets
- **AND** no theme files exist in the public repository

### Requirement: Dark Mode Support

The site SHALL support dark mode toggle for user preference.

#### Scenario: Dark mode toggle

- **WHEN** a user toggles dark mode
- **THEN** the site appearance switches to dark theme
- **AND** the preference is persisted

### Requirement: Custom Colors and Fonts

The site SHALL support customization of colors and fonts via theme configuration.

#### Scenario: Theme customization

- **WHEN** theme colors or fonts are configured
- **THEN** the site reflects the custom styling
- **AND** changes are applied consistently across pages

### Requirement: Nested Navigation Menus

The site SHALL support nested menu structures for complex navigation.

#### Scenario: Multi-level navigation

- **WHEN** configuring site navigation
- **THEN** menus can have nested child items
- **AND** navigation renders hierarchically

### Requirement: Fixed Header with Scroll Animation

The site SHALL display a fixed header that animates on scroll.

#### Scenario: Header scroll behavior

- **WHEN** the user scrolls down the page
- **THEN** the header remains fixed at the top
- **AND** visual animation indicates scroll state

### Requirement: Data-Driven Content

The site SHALL support data-driven content via JSON files in the `data/` directory.

#### Scenario: Partner and social data

- **WHEN** rendering partner logos or social links
- **THEN** data is loaded from `data/partners.json` and `data/social.json`
- **AND** templates iterate over the data

### Requirement: Static Assets

The site SHALL serve static assets from the `static/` directory including images and favicon.

#### Scenario: Static asset serving

- **WHEN** the site is built
- **THEN** contents of `static/` are copied to the output
- **AND** assets are accessible at their relative paths
