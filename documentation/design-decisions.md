# Design Decisions & Architecture Notes

This document outlines the architectural choices made during the implementation of the serverless web application. It also highlights cost optimizations and testing procedures performed in the lab environment.

## 1. Serverless Architecture (S3 + CloudFront + API Gateway + Lambda)
- **Why Serverless?** The requirement mandated "least on-going overhead" and a "cost-effective" solution. Using EC2 instances would incur costs even when idle. Serverless services (S3, Lambda, DynamoDB) scale automatically and cost nothing (or fractions of a cent) when not in use.
- **Frontend:** Hosted in an S3 bucket configured for Static Website Hosting. This is the most cost-effective way to serve HTML/CSS/JS.
- **Backend:** API Gateway (REST API) acts as the entry point for dynamic requests. It triggers Lambda functions (Python) which execute business logic.
- **Database:** DynamoDB (NoSQL) was chosen for its seamless integration with Lambda, on-demand scaling, and serverless nature.

## 2. Global Performance & Security
- **CloudFront:** Used to cache static content at Edge Locations globally.
  - *Troubleshooting Note:* The Origin Protocol was set to **HTTP only** because S3 Static Website endpoints do not support HTTPS. CloudFront handles HTTPS for the end-user, ensuring secure delivery.
- **AWS WAF:** Integrated with CloudFront to protect against common web vulnerabilities (e.g., SQL injection, XSS) and to fulfill the requirement of blocking specific countries.

## 3. WAF Testing & Proof of Concept
- To ensure the WAF rule was functioning correctly, a rule was created to block traffic from a specific country (Tested with Germany and India).
- **Result:** The request returned a `403 Forbidden` error, proving that WAF effectively blocked the traffic before it reached the CloudFront distribution or S3 origin.

## 4. CORS (Cross-Origin Resource Sharing)
- **API Gateway & Lambda:** When creating the API resource, CORS was enabled. Furthermore, the Lambda function explicitly returns the `Access-Control-Allow-Origin: *` header. This is crucial because the frontend (S3) and backend (API Gateway) are hosted on different domains, and browsers block cross-origin requests by default.

## 5. Cost Optimization (Lab Environment)
- **No NAT Gateway:** Omitted entirely, as the architecture is fully serverless and does not require private EC2 instances to access the internet.
- **No WAF DDoS Advanced Protection:** The basic WAF rules were used. The advanced Layer 7 DDoS protection (which costs ~$14/month) was not enabled to keep the lab cost near zero.
- **DynamoDB:** Used On-Demand capacity mode. This means we only pay per request, avoiding the cost of Provisioned Capacity if the table is idle.

## 6. Infrastructure as Code (Terraform)
- **Current State:** Infrastructure was provisioned manually via the AWS Console to build foundational knowledge.
- **Future Enhancement:** Terraform implementation is planned. The `infrastructure-as-code/` folder is reserved for this. To ensure honesty and accuracy, no Terraform code is included at this stage, as the author is currently undergoing formal Terraform training.