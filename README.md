# My Static Website on Amazon S3

This project hosts a static website on Amazon S3, stored in the `mital-test-website-s3` bucket within AWS. The current setup involves manually placing the website files into the S3 bucket, but a more automated approach using CI/CD pipelines can be implemented with more time.
URL: http://mital-test-website-s3.s3-website-us-east-1.amazonaws.com/

## Ideal Project Setup

The intended infrastructure setup will involve the following:

- **CI/CD Infrastructure Pipeline**: This pipeline will automate the provisioning of resources, utilizing GitHub Actions or other CI/CD tools.
- **Separate CI/CD Application Content Deployment Pipeline**: This pipeline will handle the deployment of this page and other application assets to S3 or other infrastructure components.

In a real-world production setup, the following components will be implemented:

- **Private S3 Bucket**: The S3 bucket will be set to private to prevent direct access to content.
- **CloudFront Distribution**: CloudFront will cache static content, improving performance and scalability. It will also have TLS certificate installed and AWS WAF configured for security
- **Route 53 Configuration**:
  - A public hosted zone will be created in Route 53.
  - A purchased domain will be pointed to the CloudFront distribution via Route 53 DNS records (e.g., `mitalwebsite.com`).
- **CloudFront WAF**: CloudFront will be secured with Web Application Firewall (WAF) for OWASP Top 10 protections and other custom rules.
- **CloudFront Origins**: CloudFront will define multiple origins based on subdomains or paths, such as:
  - `mitalwebsite.com/app` → Public Load Balancer
  - `mitalwebsite.com/api` → API Gateway
  - `static.mitalwebsite.com` or `/static` → Static Content

## Q&A

### What else would you do with your website if you had more time?

If given more time, the focus would be on implementing a secure and automated deployment pipeline, following a **shift-left approach** for security. This would involve adding security controls earlier in the CI/CD pipeline, ensuring that vulnerabilities are identified and mitigated before they reach production. (Apart for TLS certificate and WAF configuration)

### What alternative solutions did you consider?

While hosting static pages on an Apache web server behind an Application Load Balancer (ALB) was an option, it was deemed unnecessary and costly for this simple demo project. Authentication and authorization mechanisms would be incorporated as the website evolves.

### What would be required to make this a production-grade website?

To transform this into a production-grade website, the following management aspects would be implemented:

1. **Identity and Access Management (IAM)**:
   - Use IAM roles and policies for infrastructure and application security.
   - Integrate AWS Cognito or Ping Identity for user authentication.
   - Enforce Multi-Factor Authentication (MFA) and least-privilege access policies.
   
2. **Network Management (Security)**:
   - Set up a Virtual Private Cloud (VPC) for network isolation.
   - Implement ingress and egress controls, firewalls, VPNs, and WAF.
   - Use AWS Shield and IDS/IPS systems for enhanced DDoS protection.

3. **Application Management**:
   - Implement microservices architecture, with each service hosted in its own repository.
   - Use Docker for containerization, with multi-stage builds.
   - Deploy services to ECS (Elastic Container Service) or EKS (Elastic Kubernetes Service).

4. **Data Management**:
   - Implement secure and scalable databases for structured, semi-structured, and unstructured data.

5. **Backup Management**:
   - Establish a robust backup and disaster recovery strategy for both data and application components.

## Disclaimer

AI has been used to improve the readability of this page.
