
**!!! WORK IN PROGRESS / MAY CONTAIN ERRORS / ACTUALLY I AM PRETTY !!!**

# Frontend (Hugo Blog)

Static blog with Hugo + Congo theme. Includes visitor counter via API Gateway + Lambda.

## Prerequisites

- **Backend deployed first** - See [../backend](../backend)
- Hugo extended + Go 1.18+ (`brew install hugo go`)
- AWS CLI v2 for deployment (`brew install awscli`)

## Quick Start

```bash
# 1. Install Hugo modules
hugo mod get -u

# 2. Configure API endpoint
# Edit layouts/_partials/extend-footer.html with your API Gateway URL
# (from backend terraform output: api_gateway_url)

# 3. Set your domain
# Edit config/_default/config.toml: baseURL = 'https://yourdomain.com/'

# 4. Start local server
hugo server -D  # Drafts visible at http://localhost:1313
```

## Development Workflow

```bash
# Create new post
hugo new content/posts/my-post.md

# Edit content/posts/my-post.md (remove draft: true when ready)

# Preview locally
hugo server

# Build for production
hugo --minify

# Deploy to S3
aws sso login
aws s3 sync public/ s3://yourdomain.com --delete

# Invalidate CloudFront cache (get distribution ID from backend output)
aws cloudfront create-invalidation \
  --distribution-id YOUR_DIST_ID \
  --paths "/*"
```

## File Structure

```
frontend/
├── content/posts/              # Blog posts (Markdown)
├── layouts/_partials/          # Template overrides
│   └── extend-footer.html      # Visitor counter integration
├── config/_default/            # Site configuration
│   ├── config.toml
│   └── params.toml
├── static/                     # Static assets
├── go.mod                      # Hugo modules
└── public/                     # Generated site (gitignored)
```

## Customization

- **Theme settings**: Edit `config/_default/params.toml`
- **Override templates**: Create matching files in `layouts/`
- **Update theme**: `hugo mod get -u github.com/jpanther/congo/v2`

## Troubleshooting

- **Module errors**: Run `hugo mod get -u`
- **Counter not loading**: Check browser console, verify API URL in `extend-footer.html`
- **Changes not live**: Rebuild + sync + invalidate CloudFront cache
- **404 on CloudFront**: Check backend `cloudfront-function.tf` is deployed
- **Styles missing**: `hugo mod clean && hugo mod get -u`

## Optional: Sveltia CMS

Visual editor at `http://localhost:1313/admin` (when `hugo server` is running).
