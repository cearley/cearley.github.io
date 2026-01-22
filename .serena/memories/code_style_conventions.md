# Code Style and Conventions

## General Principles
- Prefer concise, readable code
- Use meaningful variable names
- Follow existing project conventions

## Content (Markdown)
- All content uses YAML frontmatter
- Files stored in `content/en/` directory
- Use standard Markdown with Hugo shortcodes

### Frontmatter Example
```yaml
---
title: "Page Title"
date: 2024-01-01
draft: false
categories: ["category"]
tags: ["tag1", "tag2"]
---
```

## JavaScript/Node.js (Lambda)
- Runtime: Node.js 20.x
- Module format: ESM (`.mjs` files)
- Use `export const` for handlers
- JSDoc comments for function documentation
- Testing: Mocha + Chai

### Lambda Handler Pattern
```javascript
export const lambdaHandler = async (event, context) => {
  const response = {
    statusCode: 200,
    body: JSON.stringify({ message: 'response' })
  };
  return response;
};
```

## TOML Configuration
- Hugo uses `config.toml` for site settings
- SAM uses `samconfig.toml` for deployment
- Use 2-space indentation for nested structures

## YAML (SAM Templates)
- Use CloudFormation/SAM syntax
- 2-space indentation
- Comment complex resources

## HTML Templates (Hugo)
- Follow Go template syntax
- Use partials for reusable components
- Keep templates simple, logic-light

## No Linting/Formatting Tools Configured
- No ESLint, Prettier, or similar tools detected
- Follow existing file patterns when editing
- Maintain consistency with surrounding code
