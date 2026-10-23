# AWS Serverless Web Application

## 📌 Overview
A production-grade, fully serverless web application hosted on AWS. This project demonstrates a cost-effective, highly available, and secure architecture that scales automatically with zero infrastructure overhead. It serves a global user base and protects against common web vulnerabilities.

## 🏗️ Architecture Diagram
![Architecture Diagram](./architecture/architecture-diagram.png)

## 🎯 Requirements Covered
1. **Static Content (Frontend):** HTML, CSS, and JS hosted in an S3 bucket configured as a Static Website.
2. **Dynamic Backend:** The frontend makes API calls to an API Gateway, which triggers AWS Lambda functions to perform operations on a DynamoDB database.
3. **Global Performance:** CloudFront is used to cache static content and route API calls globally.
4. **Security & Resilience:** AWS WAF is implemented to protect against common vulnerabilities (e.g., SQL injection, XSS) and block traffic from specific countries.
5. **High Availability & Scalability:** The solution is fully serverless, highly available, and scalable with zero ongoing infrastructure overhead.
6. **Cost-Effective:** Pay only for what you use (no idle EC2 instances).

## 🔧 AWS Services Used
| Service | Purpose |
|---------|---------|
| Amazon S3 | Hosting static frontend content |
| Amazon CloudFront | Global CDN and caching |
| AWS WAF | Web Application Firewall (Layer 7 security) |
| Amazon API Gateway | RESTful API management |
| AWS Lambda | Serverless compute for backend logic |
| Amazon DynamoDB | NoSQL database for dynamic data |
| AWS IAM | Access control and permissions |

## 📂 Repository Structure
```text
.
├── architecture/          # Architecture diagrams
├── screenshots/           # AWS Console screenshots (proof of implementation)
├── documentation/         # Requirements & design decisions
├── testing/               # Connectivity & validation tests
└── infrastructure-as-code/ # (Planned) Terraform implementation
```
🛠️ Implementation Summary
Manual Provisioning: All resources were manually provisioned via the AWS Management Console to ensure a deep understanding of serverless integrations.

Testing: Validated end-to-end functionality (Frontend -> API Gateway -> Lambda -> DynamoDB) and tested WAF rules by successfully blocking traffic from a specific country.

Documentation: Detailed design decisions and requirements are available in the documentation/ folder.

📸 Screenshots
All 14 implementation screenshots are available in the screenshots/ folder.

📘 Lessons Learned
Serverless architectures eliminate the need for server management and reduce costs to near zero when idle.

API Gateway CORS settings are crucial for enabling frontend-to-backend communication.

AWS WAF provides granular control over traffic (e.g., geographic blocking) without modifying the application code.

CloudFront requires HTTP-only origin protocol when pointing to an S3 Static Website endpoint.

🚀 Future Enhancements
Infrastructure as Code: Automate the entire infrastructure using Terraform.

Authentication: Add Amazon Cognito for user sign-up and sign-in.

CI/CD: Implement a pipeline (e.g., GitHub Actions) to automate frontend deployments to S3.

📄 License
This project is licensed under the MIT License - see the LICENSE file.

👤 Author
Mohammed Al-Bayati

GitHub: @MohammedAlbayati1983
