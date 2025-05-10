
# Static Website with CI/CD

This repository contains a basic static website deployed using a CI/CD pipeline powered by GitHub Actions. The site consists of HTML, CSS (Tailwind), and JavaScript files hosted on AWS S3 with automatic deployment on every push to the `main` branch.

## Features

- Static website (HTML/CSS/JS)
- Hosted on AWS S3 (Static Website Hosting enabled)
- CI/CD via GitHub Actions
- Optional CloudFront integration for CDN and HTTPS

## Project Structure

.
├── index.html
├── style.css
├── script.js
├── .github/
│ └── workflows/
│ └── deploy.yml
└── README.md



## CI/CD Pipeline

GitHub Actions is configured to deploy the website to an S3 bucket automatically on every push to the `main` branch.

### `.github/workflows/deploy.yml`

```yaml
name: Deploy Static Website

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Sync to S3
      uses: jakejarvis/s3-sync-action@v0.5.1
      with:
        args: --delete
      env:
        AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        AWS_REGION: 'ap-south-1'
        SOURCE_DIR: './'


