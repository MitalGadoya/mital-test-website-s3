Welcome to My Static Website on Amazon S3!
This page is hosted in the mital-test-website-s3 bucket in AWS. A CloudFormation stack creates this S3 bucket. Currently, placement of this file into the bucket is manual.

Ideal Project Setup
I will have CI/CD tools provisioning the infrastructure, such as GitHub workflows/actions for the application through an infrastructure pipeline.
I will have a separate CI/CD pipeline for application content deployment. This pipeline will deploy this page along with other application content to S3 or other infrastructure components.
Although the S3 bucket is public in this demo, in a real-world setup:
Make S3 bucket private.
Create CloudFront to cache static content.
Create Route53 public hosted zone and point the purchased domain to its name servers.
Create Route53 record mitalwebsite.com pointing to the CloudFront URL.
Enable CloudFront WAF configuration for OWASP Top 10 protections and other rules.
CloudFront defines an origin for the private S3 bucket and serves content securely.
CloudFront may have multiple origins based on subdomains or paths:
mitalwebsite.com/app → Public Load Balancer
mitalwebsite.com/api → API Gateway
static.mitalwebsite.com or /static → Static content
Q&A
What else would you do with your website if you had more time?
I would implement the above as a starting point for security and embed similar controls in the pipeline for a shift-left approach.
Alternative solutions considered:
I could have hosted static pages on an Apache web server fronted by an ALB, but that's expensive and unnecessary at this stage. Authentication and authorization would be added as the website grows.
What would be required to make this a production-grade website?
I would layer the website into the following management aspects for production:
Identity and Access Management(Security): IAM for infrastructure and applications, AWS Cognito or Ping Identity, MFA, and least-privilege policies.
Network Management(Security): VPC, Ingress/Egress controls, Firewalls, VPNs, WAF, AWS Shield, IDS/IPS/Web Filtering.
Application Management: Microservices hosted in separate repositories, Dockerized with multi-stage builds, deployed to ECS or EKS.
Data Management: Databases (structured, semi-structured, unstructured) in secure infrastructure.
Backup Management: Appropriate backup strategies for data and app backup & restore.
Disclaimer: AI is only used to improve readability of this page.