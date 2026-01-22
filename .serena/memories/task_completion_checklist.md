# Task Completion Checklist

## Before Completing Any Task

### 1. Code Changes
- [ ] Changes follow existing code style and patterns
- [ ] Variable/function names are meaningful
- [ ] No unnecessary code or comments added
- [ ] Changes are minimal and focused on the task

### 2. Hugo Frontend Changes
- [ ] Run `hugo server` to test locally
- [ ] Verify pages render correctly
- [ ] Check dark mode appearance (if UI changes)
- [ ] Test responsive design on different viewports

### 3. Lambda Backend Changes
- [ ] Run tests: `cd backend/hello-world && npm test`
- [ ] Test locally: `cd backend && sam local start-api`
- [ ] Verify API responses match expected format
- [ ] Check for security vulnerabilities

### 4. Content Changes
- [ ] Verify YAML frontmatter is valid
- [ ] Check Markdown renders correctly
- [ ] Verify images/assets are properly linked
- [ ] Test any internal links

### 5. Configuration Changes
- [ ] Verify TOML/YAML syntax is valid
- [ ] Test Hugo builds: `hugo`
- [ ] Test SAM validates: `cd backend && sam validate`

## Git Workflow (IMPORTANT)
Per user preferences, follow this strict protocol:

1. **Make changes locally**
2. **STOP and ask**: "Would you like me to commit these changes?"
3. **Wait for explicit permission** before running `git commit`
4. **STOP again and ask**: "Would you like me to push to GitHub?"
5. **Wait for explicit permission** before running `git push`

**Never commit or push without explicit user consent.**

## Build Commands Reference

### Hugo
```bash
hugo server          # Local dev server
hugo                 # Build to public/
```

### SAM Backend
```bash
cd backend && sam build           # Build Lambda
cd backend && sam deploy          # Deploy to AWS
cd backend/hello-world && npm test # Run tests
```

## Deployment
- **Frontend**: Auto-deploys to GitHub Pages on git push to main
- **Backend**: Manual deployment via `sam deploy`
