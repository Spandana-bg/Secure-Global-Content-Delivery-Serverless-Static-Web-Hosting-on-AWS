# Secure Cloud Portfolio: Global Static Web Hosting on AWS

A production-ready, highly available, and secure static website hosting architecture built entirely on AWS. This project leverages Amazon S3 for cost-effective object storage and AWS CloudFront as a global Content Delivery Network (CDN) to serve content with low latency and enforced HTTPS encryption.

## 🔗 Live Demo
Check out the live deployment here: [👉 https://d28ahkwiur4gxp.cloudfront.net/project-1.html](https://d28ahkwiur4gxp.cloudfront.net/project-1.html)

---

## Architecture Overview

The infrastructure relies on modern cloud security best practices by keeping the origin data completely private from the public internet, forcing all client traffic through edge caches.

* **Amazon S3:** Holds the static website source assets (`html`, `css`, `js`). Public access is completely blocked.
* **AWS CloudFront:** Serves as the Content Delivery Network (CDN) caching content at edge locations worldwide to drastically lower response times.
* **Origin Access Control (OAC):** Secures the S3 origin by restricting bucket read permissions (`s3:GetObject`) exclusively to the CloudFront service principal.
* **Security & Optimization:** Automated redirection of HTTP requests to secure HTTPS using default CloudFront SSL certificates.

---

## 🛠️ AWS Implementation Steps

### 1. Storage Configuration (Amazon S3)
* Created a private S3 bucket named `[Your S3 Bucket Name]`.
* Kept **Block Public Access** turned **ON** to prevent public data exposure.
* Uploaded all frontend static assets directly to the root level of the bucket.

### 2. Content Delivery Setup (AWS CloudFront)
* Provisioned a CloudFront Distribution pointing to the S3 bucket domain as the origin.
* Configured **Origin Access Control (OAC)** to create a trusted relationship between S3 and CloudFront.
* Updated the **S3 Bucket Policy** with the automatically generated IAM JSON policy to grant `s3:GetObject` access strictly to the CloudFront distribution identifier.
* Set the **Default Root Object** to `project-1.html`.
* Configured the **Viewer Protocol Policy** to automatically redirect `HTTP` requests to `HTTPS`.

---

## 📊 Key Learning Outcomes & Technical Skills

* **Cloud Security:** Implementing the principle of least privilege via bucket policies and disabling direct public access to backend storage.
* **Content Delivery & Edge Caching:** Understanding CDN behaviors, TTLs, caching optimizations, and utilizing cache invalidations (`/*`) to force immediate global updates.
* **Troubleshooting Core AWS Error Codes:** Debugging complex permissions issues such as AWS `403 Forbidden (AccessDenied)` errors by resolving asset folder paths and misaligned distribution behavior routing.

---

## 🚀 Technologies Used
* **Cloud Platform:** Amazon Web Services (AWS)
* **AWS Services:** Amazon S3, AWS CloudFront (OAC), IAM
* **Frontend:** HTML5, CSS3, JavaScript
* **Security protocols:** HTTPS, TLS/SSL