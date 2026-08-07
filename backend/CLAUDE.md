# Backend (AWS SAM)

```bash
# Build SAM application
cd backend && sam build

# Deploy with guided setup
sam deploy --guided

# Test locally
sam local start-api

# Invoke function locally
sam local invoke HelloWorldFunction --event events/event.json

# Run tests
cd hello-world && npm install && npm test

# View logs
sam logs -n HelloWorldFunction --stack-name backend --tail
```
