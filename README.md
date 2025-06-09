# Auto-SSL - Automated SSL Certificate Management System with GitHub Actions

[![License](https://img.shields.io/github/license/danbao/auto-ssl?style=flat-square)](LICENSE)
[![GitHub Actions](https://img.shields.io/badge/powered%20by-GitHub%20Actions-2088FF?style=flat-square&logo=github-actions)](https://github.com/features/actions)
[![Cloudflare](https://img.shields.io/badge/DNS%20Provider-Cloudflare-F38020?style=flat-square&logo=cloudflare)](https://www.cloudflare.com/)

## 🚨 Important Security Notice

> **Warning: Privacy Protection**  
> Before using this project, please ensure:
> 1. Create a **Private Repository**
> 2. Push this project's code to your private repository
> 
> ⚠️ **Never use this in public repositories, as SSL certificate private keys may be exposed**

## 📋 Project Overview

Auto-SSL is an automated SSL certificate management solution based on GitHub Actions. By integrating the `acme.sh` tool, it provides secure and reliable SSL certificate auto-issuance and renewal services for your domains.

## ✨ Core Features

- 🔐 **Automated Certificate Issuance**: Automatically issue SSL certificates based on ACME protocol
- 🔄 **Smart Renewal Management**: Daily certificate validity checks, auto-renewal within 30 days
- 📝 **Detailed Operation Logs**: Daily check reports automatically synced to `CHECK_LIST.md`
- 🌐 **Wildcard Domain Support**: Support for wildcard domain certificates
- 🔑 **Dual Encryption Algorithms**: Provides both ECDSA and RSA encryption algorithm certificates
- 💾 **Version Control Storage**: Securely store certificate files through Git commits
- ☁️ **Cloudflare Integration**: Deep integration with Cloudflare DNS API

## 🛠️ Quick Start

### Prerequisites

- Own a valid domain name
- Domain hosted on Cloudflare
- GitHub account with repository management permissions

### Configuration Steps

#### 1️⃣ Domain Preparation

Ensure you own a domain name. If you need to register one, you can use the following registrars:
- Alibaba Cloud
- Tencent Cloud
- GoDaddy
- Namecheap, etc.

#### 2️⃣ Cloudflare Domain Hosting

Migrate your domain DNS resolution service to Cloudflare:
1. Register a [Cloudflare](https://www.cloudflare.com/) account
2. Add your domain
3. Follow the instructions to modify nameservers
4. Wait for DNS propagation to complete

#### 3️⃣ Obtain Cloudflare API Credentials

**Get API Token:**
1. Visit [Cloudflare API Token Management Page](https://dash.cloudflare.com/profile/api-tokens)
2. Click "Create Token"
3. Select custom token and configure the following permissions:
   - **Permissions**: `Zone:Zone:Read`, `Zone:DNS:Edit`
   - **Zone Resources**: Select target domain

![API Token Configuration Example](https://github.com/danbao/auto-ssl/assets/4090783/ea014646-8cbe-4064-a764-b45281e42e55)

**Get Account ID:**
1. Log into Cloudflare dashboard
2. Select any hosted domain
3. Find "Account ID" in the right sidebar

![Account ID Location](https://github.com/danbao/auto-ssl/assets/4090783/d1d86260-89ce-4179-a0c2-e8a2361e627f)

#### 4️⃣ Configure GitHub Secrets

Set the following secret variables in your GitHub repository:

**Path:** `Settings` → `Security` → `Secrets and variables` → `Actions`

| Variable Name | Description | Example |
|---------------|-------------|---------|
| `CF_TOKEN` | Cloudflare API Token | `1234567890abcdef...` |
| `CF_ACCOUNT_ID` | Cloudflare Account ID | `abcdef1234567890...` |
| `EMAIL` | Email address for certificate application | `admin@example.com` |

![GitHub Secrets Configuration](https://github.com/danbao/auto-ssl/assets/4090783/e3ea47d8-7b3e-4605-94ee-689e6bb6ca45)

#### 5️⃣ Set GitHub Actions Permissions

**Path:** `Settings` → `Actions` → `General` → `Workflow permissions`

Select: **Read and write permissions**

![Actions Permission Settings](https://github.com/danbao/auto-ssl/assets/4090783/abb42eb0-fd78-4417-bf07-9cf090ee7a2c)

#### 6️⃣ Configure Target Domains

Edit the `cloudflare_domains_list.txt` file in your repository:
```text
example.com
*.example.com
subdomain.example.com
```
> Enter one domain per line, wildcard domains are supported

#### 7️⃣ Manually Trigger First Run

1. Go to the `Actions` tab
2. Select the corresponding workflow
3. Click "Run workflow" to trigger manually

## 📊 Operation Status

- **Certificate Check**: Automatically executes daily at UTC 00:00
- **Renewal Threshold**: Auto-renewal when certificate validity is less than 30 days
- **Status Reports**: Detailed logs recorded in `CHECK_LIST.md` file

## 🔧 Troubleshooting

### Common Issues

**Q: Certificate application failed?**
A: Please check:
- Cloudflare API Token permission settings
- Domain DNS record correctness
- GitHub Secrets configuration completeness

**Q: Workflow execution failed?**
A: Please review:
- Actions run logs
- Network connection status
- API call limits

### Get Support

If you encounter issues, please:
1. Check the [Issues](../../issues) page
2. Submit detailed error logs
3. Describe your configuration environment

## 📄 License

This project is licensed under an open source license. Please refer to the [LICENSE](LICENSE) file for details.