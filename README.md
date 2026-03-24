# 🚀 Portfolio Hosting: AWS S3 + CloudFront Architecture

A high-performance, cost-effective, and secure approach to hosting a static portfolio website using AWS serverless infrastructure.

---

## 🏗️ Architecture Overview

This project utilizes a **Serverless Static Web Hosting** model. By removing the need for a traditional web server, the site achieves high availability with near-zero maintenance.

* **Amazon S3:** Functions as the origin server, storing static assets (HTML, CSS, JS, and images).
* **Amazon CloudFront:** Acts as the Content Delivery Network (CDN) layer, caching content at Edge Locations worldwide for low-latency delivery and managed HTTPS.
* **AWS IAM & OAC:** * **Origin Access Control (OAC):** Restricts bucket access so the site is *only* reachable via CloudFront.
    * **IAM Policies:** A specific bucket policy is applied to grant the CloudFront service principal `s3:GetObject` permissions, ensuring secure, identity-based access control.

---
<img width="2537" height="1385" alt="image" src="https://github.com/user-attachments/assets/211ac011-62cf-433e-b14c-e9dd151caf02" />

## 💡 Why This Approach?

| Feature | Benefit |
| :--- | :--- |
| **Granular Security** | IAM policies ensure that no "anonymous" users can browse your S3 bucket directly. |
| **Performance** | Content is served from the server physically closest to the visitor via CloudFront. |
| **Scalability** | Handles traffic spikes automatically without any manual infrastructure scaling. |
| **Cost** | Extremely low-cost; fits well within the AWS Free Tier for personal use. |

---

## 🛠️ Roadmap for Improvement

To modernize the workflow and move away from manual uploads, the following enhancements are planned:

### 1. Automation via CI/CD (GitHub Actions)
Currently, deployments are manual. I plan to implement a **GitHub Actions** workflow:
* **The Workflow:** On every `git push` to `main`, the runner will build the site, sync files to S3 using an IAM User with limited programmatic access, and trigger a CloudFront cache invalidation.

### 2. Transition to AWS Amplify
Migrating to **AWS Amplify Hosting** to streamline the developer experience:
* **Atomic Deployments:** Ensures the site only updates if the build is successful.
* **Preview Environments:** Automatically generates a unique URL for every Pull Request to test changes before merging.

### 3. Infrastructure as Code (IaC)
Using **Terraform** or **AWS CDK** to define the infrastructure. This allows the IAM roles, S3 bucket, and CloudFront settings to be version-controlled and easily reproducible.

---


1. **Sync files to S3:**
   ```bash
   aws s3 sync ./dist s3://your-portfolio-bucket-name --delete
