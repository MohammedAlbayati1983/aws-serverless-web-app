# Connectivity & Validation Tests

The following tests were performed to validate the serverless architecture, security configurations, and end-to-end functionality of the application.

| # | Test Description | Expected Result | Status |
|---|------------------|-----------------|--------|
| 1 | S3 Static Website accessible via S3 endpoint | HTML page loads successfully | ✅ Passed |
| 2 | API Gateway POST request directly (via Postman/CLI) | Returns 200 OK & saves to DynamoDB | ✅ Passed |
| 3 | Frontend to API Gateway (CORS check) | Browser successfully sends request without CORS error | ✅ Passed |
| 4 | DynamoDB Data Verification | Item inserted via Lambda appears in DynamoDB table | ✅ Passed |
| 5 | CloudFront Distribution Access | Website loads via CloudFront domain name | ✅ Passed |
| 6 | CloudFront Default Root Object | Opening CloudFront URL loads `index.html` automatically | ✅ Passed |
| 7 | WAF Country Blocking | Traffic from blocked country returns 403 Forbidden | ✅ Passed |
| 8 | S3 Origin Accessibility (WAF Bypass Test) | S3 direct URL still works (WAF protects CloudFront only) | ✅ Passed |

## Key Validations:
- **Serverless Integration:** Verified that the frontend (S3) successfully communicates with the backend (API Gateway -> Lambda -> DynamoDB).
- **Security (WAF):** Validated that the WAF rule effectively blocks requests based on geographical location without affecting the application code.
- **High Availability:** Validated that CloudFront serves the cached content globally.