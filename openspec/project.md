# Project Context

## Purpose
Personal portfolio website for Craig Earley Software, LLC. The site showcases services, portfolio work, blog posts, and provides contact functionality. Deployed at `craigearley.software`.

## Tech Stack

### Frontend
- **Hugo** (v0.154.0) - Static site generator
- **Hugo Advance Theme** - Premium theme with dark mode support
- **Markdown** - Content format with YAML frontmatter
- **CSS/SCSS** - Styling via theme assets

### Backend
- **AWS SAM** - Serverless Application Model
- **AWS Lambda** - Node.js 20.x runtime
- **AWS API Gateway** - REST API endpoints
- **AWS S3** - Static asset hosting
- **AWS CloudFront** - CDN distribution

### Deployment
- **GitHub Pages** - Frontend hosting (via GitHub Actions)
- **AWS SAM CLI** - Backend deployment

## Project Conventions

### Code Style
- Prefer concise, readable code
- Use meaningful variable names
- Follow existing project conventions
- No linting/formatting tools configured - maintain consistency with surrounding code

### Content Format
- All content uses YAML frontmatter
- Files stored in `content/en/` directory
- Use standard Markdown with Hugo shortcodes

### JavaScript/Node.js (Lambda)
- Runtime: Node.js 20.x
- Module format: ESM (`.mjs` files)
- Use `export const` for handlers
- JSDoc comments for function documentation
- Testing: Mocha + Chai

### Architecture Patterns
- **Hybrid Approach**: Static frontend with serverless backend for dynamic features
- **Single Lambda Pattern**: Current implementation uses a simple "hello world" template
- **CDN-First**: CloudFront handles content delivery and API routing

### Testing Strategy
- Lambda tests located in `backend/hello-world/tests/`
- Run tests with `cd backend/hello-world && npm install && npm test`
- Hugo site testing via `hugo server` for local verification

### Git Workflow
- **CRITICAL**: Never commit or push without explicit user consent
- Two separate permission gates: one for commit, one for push
- Frontend auto-deploys to GitHub Pages on push to `main`
- Backend requires manual `sam deploy`

## Domain Context

### Content Types
- **Posts**: Blog articles with categories, tags, and publication dates
- **Portfolio**: Design work, GitHub projects, research publications
- **Services**: Business service descriptions (Branding, Web Design)
- **Team**: Staff profiles with bios and role information
- **Work**: Detailed case studies and project documentation
- **Pages**: Standard website pages (About, Privacy Policy, Terms)
- **Authors**: Author profiles and contributor information
- **Contact**: Contact forms and success/thank you pages

### Key URLs
- Production: https://craigearley.software
- Backend API: CloudFront → API Gateway → Lambda

## Important Constraints

### Deployment
- Hugo version locked to v0.154.0 (per GitHub Actions workflow)
- Backend deployment requires AWS credentials configured
- Custom domain configured via CNAME file

### Security
- Avoid introducing OWASP top 10 vulnerabilities
- Never commit sensitive files (.env, credentials)
- CodeQL analysis runs via GitHub Actions

## External Dependencies

### AWS Services
- S3 (static hosting)
- CloudFront (CDN)
- Lambda (serverless compute)
- API Gateway (REST endpoints)

### CI/CD
- GitHub Actions for Hugo deployment
- GitHub Actions for CodeQL security analysis

### Theme
- Hugo Advance theme in `themes/hugo-advance/`
- Supports dark mode, custom colors, nested menus, fixed header