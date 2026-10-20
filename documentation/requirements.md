# Project Requirements

Design a cost-effective solution to serve the static content of a website hosted in AWS. The solution should cater to a global user base. The solution must be scalable, highly available, resilient against malicious internet traffic, and protected from new common vulnerabilities. The solution must be able to block traffic from certain countries and should require the least on-going overhead.

### Extended Requirements (Based on Architecture Design):
- **Dynamic Backend:** The frontend (HTML/CSS/JS) must be able to send API requests to a backend service.
- **Decoupling:** The backend must be serverless and use API Gateway + Lambda to process requests.
- **Database:** Data must be stored in a NoSQL database (DynamoDB).