# Content Management

## Purpose

The site uses Markdown files with YAML frontmatter organized into distinct content types for portfolio, blog, and business information.

## Requirements

### Requirement: Markdown with YAML Frontmatter

All content files SHALL be written in Markdown format with YAML frontmatter for metadata.

#### Scenario: Standard content file format

- **WHEN** creating a new content file
- **THEN** it uses `.md` extension
- **AND** begins with YAML frontmatter delimited by `---`
- **AND** includes at minimum `title` and `date` fields

### Requirement: Blog Posts

The site SHALL support blog posts with categories, tags, and publication dates stored in `content/en/posts/`.

#### Scenario: Creating a blog post

- **WHEN** a new blog post is created in `content/en/posts/`
- **THEN** it appears in the blog listing
- **AND** can be filtered by categories and tags

### Requirement: Portfolio Content

The site SHALL organize portfolio content into three sections: design work, GitHub projects, and research publications.

#### Scenario: Portfolio sections

- **WHEN** viewing the portfolio
- **THEN** content is organized under `content/en/portfolio/`
- **AND** includes `design/`, `github/`, and `research/` subdirectories

### Requirement: Service Descriptions

The site SHALL display business service offerings for branding and web design.

#### Scenario: Service pages

- **WHEN** viewing services
- **THEN** content is served from `content/en/services/`
- **AND** includes `branding/` and `web-design/` sections

### Requirement: Team Profiles

The site SHALL display team member profiles with bios and role information.

#### Scenario: Team member listing

- **WHEN** viewing team information
- **THEN** content is served from `content/en/team/`
- **AND** each member has a profile with bio

### Requirement: Static Pages

The site SHALL include standard website pages for about, privacy policy, terms and conditions, and disclaimer.

#### Scenario: Static page access

- **WHEN** accessing standard pages
- **THEN** content is served from `content/en/pages/`
- **AND** includes about, disclaimer, privacy policy, and terms pages

### Requirement: Contact Functionality

The site SHALL provide contact page and success confirmation page.

#### Scenario: Contact flow

- **WHEN** a user submits the contact form
- **THEN** they are redirected to a success page
- **AND** contact content is managed in `content/en/contact/`

### Requirement: Author Profiles

The site SHALL support author profiles for content attribution.

#### Scenario: Author attribution

- **WHEN** content has an author
- **THEN** author information is retrieved from `content/en/authors/`

### Requirement: Work Case Studies

The site SHALL display detailed project case studies and documentation.

#### Scenario: Case study pages

- **WHEN** viewing work/projects
- **THEN** detailed case studies are served from `content/en/work/`
