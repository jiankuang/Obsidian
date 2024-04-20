![[Deploying Single Page Application on AWS.png]]

### S3 
Create a buck same as the domain name. 
Turn off block all public access for now. Since we want to host a website for everyone to access. 
![[Turn off Block Public Access settings.png]]
#### S3 Policies 
Give people read access only for viewing the website. 
Permissions -> Bucket policy -> Edit 
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "s3:GetObject"
      ],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::${bucketname}/*",
      "Principal": "*"
    }
  ]
}
```

### S3 bucket properties 
Edit properties to host static website 
Properties -> Static website hosting -> Edit -> Enable 
Index document: index.html 
Save changes. 
Now you get a domain like `http://${bucketname}.s3-website-us-east-1.amazonaws.com`. 
### Deploy App with the AWS CLI 
Install AWS CLI https://aws.amazon.com/cli/
You can set up the AWS CLI by running `aws configure`
#### Build the app 
Remember to run `npm install` first 
`npm run build` to build the app

`aws s3 cp ${buildFolderName} s3://${s3bucketname} --recursive`

Now, visit the domain link you got, `http://${bucketname}.s3-website-us-east-1.amazonaws.com` You should be able to see your static website. 

### Route 53 
Register a domain name. Will take sometime for the domain to be live. 
After the domain is live. Go to `Hosted Zones > Your Domain name > Create record` 
Turn on alias so your domain can point to your S3 bucket. 
Route traffic to, 
Choose endpoint: "Alias to S3 website endpoint". 
Choose region: "us-east-1" (whichever region your s3 bucket in)
Enter s3 endpoint: "s3-website-us-east-1.amazonaws.com"
### AWS Certificate Manager (ACM)
This allows us to have HTTPS traffic. 
request a certificate 
After creating a certificate with the domain name, click "Create records in Route 53"
### CloudFront
* We're going to create a new CloudFront distribution 
* We're going to point it to our static website on S3
* We'll add our domain names 
* We'll set up gzipping for our assets 
* We'll set a default root object 
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