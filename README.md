#STATIC-WEBSITE-HOSTING-USING-S3

🌐 AWS Static Portfolio Hosting (S3 + CloudFront)
📌 Project Overview

This project demonstrates how to deploy a personal portfolio website using AWS S3 for static hosting and CloudFront as a CDN layer.

The goal is to create a fast, scalable, and secure static website while understanding the fundamentals of AWS hosting and permissions.

🧩 Services Used
Amazon S3
Used to store and serve static files (HTML, CSS, JS) like a web server.
AWS IAM (Identity and Access Management)
Controls permissions and ensures only the required access is granted.
Amazon CloudFront (CDN) (Optional but Recommended)
Improves performance, enables HTTPS, and distributes content globally.
🚀 Features
Static website hosting using S3
Secure access configuration using IAM policies
Global content delivery using CloudFront
HTTPS support via CloudFront
Beginner-friendly AWS architecture
🛠️ Architecture
User → CloudFront (CDN) → S3 Bucket (Static Website)
                    ↑
                  IAM (Access Control)
📂 Project Structure
/portfolio-project
│── index.html
│── style.css
│── script.js
│── assets/
│── README.md
⚙️ Setup Guide
🔹 Phase 1: Create S3 Bucket
Create a new S3 bucket
Disable "Block all public access"
Enable Static Website Hosting
Upload your portfolio files
🔹 Phase 2: Configure Bucket Policy

Allow public read access using a policy like:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": ["s3:GetObject"],
      "Resource": ["arn:aws:s3:::YOUR-BUCKET-NAME/*"]
    }
  ]
}
🔹 Phase 3: Access Website

Use the S3 Website Endpoint URL to view your live site.

🔹 Phase 4: (Important Concept)

⚠️ Common Beginner Mistake

Do NOT select the S3 bucket directly in CloudFront origin settings.

Instead:

Copy and paste the S3 Website Endpoint URL manually
❌ Wrong:
Selecting bucket from dropdown
✅ Correct:

Using website endpoint like:

http://your-bucket-name.s3-website-region.amazonaws.com

👉 Why this matters:

The dropdown uses the REST API endpoint, which breaks static website routing (e.g., index.html, error pages).
🔹 Phase 5: CloudFront Distribution
Create a CloudFront distribution
Set origin as your S3 website endpoint
Enable:
Redirect HTTP → HTTPS
Wait for deployment (~15–20 minutes)
🔹 Phase 6: Access via CloudFront

Use the generated CloudFront URL:

https://your-distribution-id.cloudfront.net

🎉 Your site is now:

Faster
Globally distributed
HTTPS enabled

One main point to be notes is that  , whenever I update the existing codes , I have to upload it everytime manually in the S3 bucket , so that it rewrites and the new changes will be displayed , which can be automated using AWS Amplify / CI/CD Pipelines.

🔮 Future Improvements
🚀 1. AWS Amplify Integration
Automatic deployment from GitHub
Built-in CI/CD
Easy custom domain setup

Benefits:

No manual uploads
Continuous updates on code push
Beginner-friendly deployment pipeline
