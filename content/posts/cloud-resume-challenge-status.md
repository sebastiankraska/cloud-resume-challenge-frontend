---
title: Cloud Blog Challenge - What's done, what's not
date: 2025-11-10T16:51:00+0100
description: Two tables. What's done, what's not.
draft: false
tags:
  - AWS
  - Cloud Resume Challenge
  - Progress
categories:
  - Technology
series:
  - Cloud Resume Challenge
author: ''
feature: ''
lastmod: ''
showTableOfContents: true
showReadingTime: true
showWordCount: true
---
The Cloud Resume Challenge has [16 steps](https://cloudresumechallenge.dev/docs/the-challenge/aws/). The Terraform extension [adds 12 more](https://cloudresumechallenge.dev/docs/extensions/terraform-getting-started/). Below is where I actually stand.

## Original Challenge (16 Steps)

| # | Step | Current State | Notes |
| --- | --- | --- | --- |
| 1 | Certification | ❌ Skipped | Chose hands-on over credentials |
| 2 | HTML | ✅ Done | Hugo instead of raw HTML |
| 3 | CSS | ✅ Done | Congo theme + custom styles |
| 4 | Static Website | ✅ Done | S3 + CloudFront OAC |
| 5 | HTTPS | ✅ Done | ACM certificate (us-east-1) |
| 6 | DNS | ✅ Done | Route 53 → sebastiankraska.com |
| 7 | JavaScript | ✅ Done | Fetches API on page load |
| 8 | Database | ✅ Done | DynamoDB, on-demand billing |
| 9 | API | ✅ Done | HTTP API, CORS locked |
| 10 | Python | ✅ Done | 32 lines, boto3 |
| 11 | Tests | ✅ Done | Testing with "pytest" and "requests" |
| 12 | IaC | ✅ Done | Terraform (not SAM) |
| 13 | Source Control | ✅ Done | Two repos (frontend/backend) |
| 14 | CI/CD (Backend) | ✅ Done  | Terraform via Github Actions (OIDC) |
| 15 | CI/CD (Frontend) | ❌ Missing | Manual aws s3 sync |
| 16 | Blog Post | 🟡 In Progress | Publishing now |

**Score: 13/16 complete**

## Terraform Extension (12 Steps)

| # | Step | Current State | Notes |
| --- | --- | --- | --- |
| 1 | Configure Credentials | ✅ Done | AWS CLI configured |
| 2 | Provider Config | ✅ Done | AWS provider in versions.tf |
| 3 | Initialize Terraform | ✅ Done | S3 backend for stat |
| 4 | Convert Storage | ✅ Done | S3 bucket in Terraform |
| 5 | Review & Apply Storage | ✅ Done | `terraform plan` shows clean |
| 6 | Examine State | ✅ Done | S3 remote backend |
| 7 | HTTPS IaC | ✅ Done | CloudFront + ACM |
| 8 | DNS IaC | ✅ Done | Route 53 config |
| 9 | Database IaC | ✅ Done | DynamoDB table |
| 10 | API IaC | ✅ Done | Lambda + API Gateway |
| 11 | Modify Resources | ✅ Done | Tested updates |
| 12 | Blog Documentation | 🟡 In Progress | Architecture + Terraform posts done |

**Score: 11/12 complete**

## What This Means

Infrastructure works. `terraform plan` shows no drift. Counter increments. HTTPS resolves.

CI/CD for backend exist. Every push to main lets Github "terraform" AWS. Github and AWS communicate via OpenID Connect (OIDC). The IAM Role that Github assumes uses least privilege permissions (though I have to say: it does need quite a few permissions)

Tests exist. Playwright/Cypress are overkill from my POV. I just used "requests" and "pytest". 

Burn-down is unproven. I have not tested `terraform destroy` → `terraform apply`. (I somewhat tested it during the switch from a subdomain to the main domain. I am pretty sure I will experience again how disabling and trying to delete Clound Distribution takes so long that Terraform will timeout - I will find out soon)

## Why I Deviated

**Skipped: AWS Cloud Practitioner cert**

Interviews care about hands-on skills. Cert is noise. I consider doing the "AWS Solutions Architect Associate" certification.

**Changed: SAM → Terraform**

Terraform is industry standard. SAM is vendor lock-in.

**Changed: Raw HTML → Hugo**

Hugo is production tooling. I know HTML, CSS and JS from other projects.

## What's Next

1. Frontend CI/CD
2. Burn-down test
3. Terraform comments
4. Finish posts

optional:

- Attach API Gateway to CloudWatch (Monitoring / Observability)
- Check if rate-limiting makes sense to save costs (I think AWS Free Tiers are pretty capable, but am not sure)

---

<sub>🤖 This content's AI Influence Levels ist AIL3: A human fully described the structure and sources, then an AI researched and wrote the post (and then a human edited that again). ([About AI Influence Level](https://danielmiessler.com/blog/ai-influence-level-ail)) </sub>
