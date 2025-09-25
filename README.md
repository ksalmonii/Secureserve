# 🔒 SecureServe: Zero-Trust Static Website on AWS

A production-ready, secure, cost-optimized static website deployed on AWS using S3, CloudFront, and IAM best practices. Built to demonstrate core **AWS Solutions Architect – Associate (SAA)** concepts — especially **"Design Secure Architectures."**

> ✅ **Fully private** — no public S3 access  
> ✅ **Encrypted at rest** — SSE-S3 enabled  
> ✅ **Encrypted in transit** — HTTPS enforced  
> ✅ **Zero operational overhead** — fully managed services  
> ✅ **Cost**: ~$0.50/month (well within AWS Free Tier)

---

## 🔐 Security Features

### 1. **S3 Block Public Access = ON**  
- Prevents accidental public exposure of objects  
- Enforced at bucket and account level

### 2. **Origin Access Identity (OAI)**  
- CloudFront accesses S3 **only via OAI**  
- Direct S3 access = `403 Forbidden`  
- No IAM users, access keys, or public policies

### 3. **SSE-S3 Encryption (Server-Side Encryption with Amazon S3-Managed Keys)**  
- All objects **automatically encrypted at rest**  
- Keys managed by AWS — no key rotation or management needed  
- **Free** and enabled by default for new buckets (but explicitly enabled here)

> 💡 **What is SSE-S3?**  
> When you enable SSE-S3, AWS encrypts your S3 objects using **AES-256** before saving them to disk. The encryption keys are **fully managed by AWS** — you don’t create, rotate, or store them. It’s the simplest, most secure way to encrypt S3 data at rest — and it’s **free**.

### 4. **HTTPS Enforcement**  
- CloudFront redirects HTTP → HTTPS  
- Uses AWS Certificate Manager (ACM) for free TLS certificates

### 5. **Monitoring & Governance**  
- **IAM Access Analyzer**: Continuously monitors for public resource exposure  
- **CloudWatch**: Logs and metrics for CloudFront requests

---

## 🚀 How to Deploy (Manual Setup)

> ⚠️ This project uses **AWS Console** (no Terraform/CLI) for learning clarity.

1. **Create S3 bucket**  
   - Name: `secureserve-yourname`  
   - Region: `ca-central-1` (or your preferred region)  
   - **Uncheck "Block all public access"** (we’ll lock it down properly)

2. **Upload `index.html`**  
   - Add your static HTML file to the bucket root

3. **Enable SSE-S3 Encryption**  
   - Go to **S3 → your bucket → Properties → Default encryption**  
   - Click **Edit** → Select **"S3-managed keys (SSE-S3)"** → **Save**

4. **Create CloudFront Distribution**  
   - Origin domain: your S3 bucket (`secureserve-yourname.s3.region.amazonaws.com`)  
   - **Origin access**: "Legacy access identities" → Create OAI  
   - ✅ **Check "Yes, update the bucket policy"**  
   - Default root object: `index.html`  
   - Viewer protocol policy: "Redirect HTTP to HTTPS"

5. **Lock Down S3**  
   - Go to **S3 → Permissions → Block public access** → **Enable all settings**

6. **Enable Monitoring**  
   - **IAM Access Analyzer**: Create analyzer for S3 buckets  
   - **CloudWatch**: Metrics auto-enabled for CloudFront



## 🎯 Why This Matters for AWS SAA

This project directly maps to **4 SAA domains**:

| Domain | Concept Demonstrated |
|--------|----------------------|
| **🔐 Design Secure Architectures** | OAI, Block Public Access, SSE-S3, HTTPS, Access Analyzer |
| **⚡ Design High-Performing** | CloudFront caching, global edge |
| **💰 Design Cost-Optimized** | S3 + CloudFront = pennies, no servers |
| **🛡️ Design Resilient** | No single point of failure, global distribution |

---

## 🌍 Built By
Keith salmon II  — Future Global Cloud Architect  
🔗 [LinkedIn](https://www.linkedin.com/in/keith-s-b59aa124/ | 📧 ksalmonii@gmail.com

> ✨ **"Security isn’t a feature — it’s the foundation."**
