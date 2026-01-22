# Project Overview

## Purpose
Personal portfolio website for Craig Earley Software, LLC. The site showcases services, portfolio work, blog posts, and provides contact functionality. Deployed at `craigearley.software`.

## Tech Stack

### Frontend
- **Hugo** (v0.154.0) - Static site generator
- **Hugo Advance Theme** - Premium theme with dark mode support (via Hugo Modules)
- **Hugo Modules** - Imports theme and content from private repos
- **Markdown** - Content format with YAML frontmatter
- **CSS/SCSS** - Styling via theme assets

### Private Repositories (Hugo Modules)
- `github.com/cearley/private-hugo-theme` - Licensed Hugo Advance theme
- `github.com/cearley/private-content` - Blog posts, portfolio projects, case studies

Content from private-content is mounted to:
- `articles/*` → `content/en/posts`
- `portfolio/projects` → `content/en/portfolio/github`
- `portfolio/case-studies` → `content/en/work`

### Backend
- **AWS SAM** - Serverless Application Model
- **AWS Lambda** - Node.js 20.x runtime
- **AWS API Gateway** - REST API endpoints
- **AWS S3** - Static asset hosting
- **AWS CloudFront** - CDN distribution

### Deployment
- **GitHub Pages** - Frontend hosting
- **AWS SAM CLI** - Backend deployment

## Key URLs
- Production: https://craigearley.software
- Backend API: CloudFront → API Gateway → Lambda

## Languages Detected
- TypeScript (theme assets)
- JavaScript/Node.js (Lambda functions)
- YAML (SAM templates, Hugo config)
- TOML (Hugo configuration)
- Markdown (content)
- HTML (Hugo templates)
