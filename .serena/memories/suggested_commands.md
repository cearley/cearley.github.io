# Suggested Commands

## Hugo Site Development

### Install Hugo (if not installed)
```bash
brew install hugo
```

### Development Server
```bash
hugo server
```
Starts local dev server with live reload at http://localhost:1313

### Build Site
```bash
hugo
```
Builds static site to `public/` directory

### Build for Production
```bash
hugo --environment production
```

## Hugo Modules

### Update All Modules (theme + content)
```bash
hugo mod get -u
```

### Update Specific Module
```bash
hugo mod get -u github.com/cearley/private-content
```

### Show Module Graph
```bash
hugo mod graph
```

### Verify Modules
```bash
hugo mod verify
```

### Development Workflow (Content Changes)
1. Edit content in `github.com/cearley/private-content`
2. Push changes to private-content repo
3. In this repo: `hugo mod get -u`
4. Test: `hugo server`
5. Commit `go.mod` and `go.sum`
6. Push to deploy

### Local Development with Content
Add to `go.mod` temporarily:
```
replace github.com/cearley/private-content => /path/to/local/private-content
```
Remove before committing.

## AWS SAM Backend

### Prerequisites
```bash
brew install aws-sam-cli
aws configure  # Set up AWS credentials
```

### Build SAM Application
```bash
cd backend && sam build
```

### Deploy with Guided Setup (first time)
```bash
cd backend && sam deploy --guided
```

### Deploy (subsequent)
```bash
cd backend && sam deploy
```

### Test Lambda Locally
```bash
cd backend && sam local start-api
```

### Invoke Single Function
```bash
cd backend && sam local invoke HelloWorldFunction --event events/event.json
```

### Run Lambda Tests
```bash
cd backend/hello-world && npm install && npm test
```

### View Lambda Logs
```bash
sam logs -n HelloWorldFunction --stack-name backend --tail
```

## GitHub Pages Deployment
The site deploys to GitHub Pages. After pushing to main:
```bash
git add .
git commit -m "message"
git push origin main
```
GitHub Pages will automatically build and deploy the Hugo site.

## Git Commands (macOS/Darwin)
```bash
git status          # Check current status
git add .           # Stage all changes
git commit -m "msg" # Commit changes
git push            # Push to remote
git pull            # Pull latest changes
```

## System Utilities (Darwin/macOS)
```bash
ls -la              # List files with details
cd <dir>            # Change directory
find . -name "*.md" # Find files by pattern
grep -r "pattern" . # Search in files
open .              # Open current directory in Finder
```
