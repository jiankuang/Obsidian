### Deploy App with the AWS CLI 
### Build a CI Pipeline 
Create a Policy `DeployStaticAssets` with CloudFront Write permission and S3 List, Write permission. 
Create a User `BuildProcess` with `DeployStaticAssets` policy. 

Go to your Github repository you want to deploy. 
Go to Actions, click "setup action for yourself", which will create a `main.yml` file. 

```yml
name: Deploy Website

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      # Checkout your repository under $GITHUB_WORKSPACE, so your job can access
      - name: Checkout Repository
        uses: actions/checkout@v2
      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
      - name: Install modules
        run: npm ci
      - name: Build application
        run: npm run build
      - name: Deploy to S3
        run: aws s3 sync ./build/ s3://${{ secrets.BUCKET_ID }}
      - name: Create CloudFront invalidation
        run: aws cloudfront create-invalidation --distribution-id ${{ secrets.DISTRIBUTION_ID }} --paths "/*"
```

Go to Settings -> Secrets and variables -> Actions, create new repository secrets. 