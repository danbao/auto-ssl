# Auto-SSL - 基于 GitHub Actions 的自动化 SSL 证书管理系统

[![License](https://img.shields.io/github/license/danbao/auto-ssl?style=flat-square)](LICENSE)
[![GitHub Actions](https://img.shields.io/badge/powered%20by-GitHub%20Actions-2088FF?style=flat-square&logo=github-actions)](https://github.com/features/actions)
[![Cloudflare](https://img.shields.io/badge/DNS%20Provider-Cloudflare-F38020?style=flat-square&logo=cloudflare)](https://www.cloudflare.com/)

## 🚨 重要安全提示

> **警告：隐私保护**  
> 使用本项目前，请务必：
> 1. 创建一个**私有仓库（Private Repository）**
> 2. 将本项目代码推送到您的私有仓库
> 
> ⚠️ **切勿在公开仓库中使用，否则SSL证书私钥将面临泄露风险**

## 📋 项目简介

Auto-SSL 是一个基于 GitHub Actions 的自动化 SSL 证书管理解决方案，通过集成 `acme.sh` 工具，为您的域名提供安全、可靠的 SSL 证书自动申请与续期服务。

## ✨ 核心特性

- 🔐 **自动化证书申请**：基于 ACME 协议自动申请 SSL 证书
- 🔄 **智能续期管理**：每日检查证书有效期，30天内自动续期
- 📝 **详细运行日志**：每日检查报告自动同步至 `CHECK_LIST.md`
- 🌐 **泛域名支持**：支持申请通配符域名证书
- 🔑 **双重加密算法**：同时提供 ECDSA 和 RSA 两种加密算法证书
- 💾 **版本控制存储**：通过 Git 提交安全存储证书文件
- ☁️ **Cloudflare 集成**：深度集成 Cloudflare DNS API

## 🛠️ 快速开始

### 前置要求

- 拥有有效域名
- 域名已托管至 Cloudflare
- GitHub 账户及仓库管理权限

### 配置步骤

#### 1️⃣ 域名准备

确保您已拥有域名。如需申请，可通过以下注册商：
- 阿里云
- 腾讯云  
- GoDaddy
- Namecheap 等

#### 2️⃣ Cloudflare 域名托管

将您的域名 DNS 解析服务迁移至 Cloudflare：
1. 注册 [Cloudflare](https://www.cloudflare.com/) 账户
2. 添加您的域名
3. 按照指引修改域名服务器
4. 等待 DNS 传播完成

#### 3️⃣ 获取 Cloudflare API 凭证

**获取 API Token：**
1. 访问 [Cloudflare API Token 管理页面](https://dash.cloudflare.com/profile/api-tokens)
2. 点击「创建令牌」
3. 选择自定义令牌，配置以下权限：
   - **权限**：`Zone:Zone:Read`, `Zone:DNS:Edit`
   - **区域资源**：选择目标域名

![API Token 配置示例](https://github.com/danbao/auto-ssl/assets/4090783/ea014646-8cbe-4064-a764-b45281e42e55)

**获取 Account ID：**
1. 登录 Cloudflare 控制台
2. 选择任意托管域名
3. 在右侧边栏找到「Account ID」

![Account ID 位置](https://github.com/danbao/auto-ssl/assets/4090783/d1d86260-89ce-4179-a0c2-e8a2361e627f)

#### 4️⃣ 配置 GitHub Secrets

在您的 GitHub 仓库中设置以下机密变量：

**路径：** `Settings` → `Security` → `Secrets and variables` → `Actions`

| 变量名 | 描述 | 示例 |
|--------|------|------|
| `CF_TOKEN` | Cloudflare API Token | `1234567890abcdef...` |
| `CF_ACCOUNT_ID` | Cloudflare Account ID | `abcdef1234567890...` |
| `EMAIL` | 证书申请邮箱地址 | `admin@example.com` |

![GitHub Secrets 配置](https://github.com/danbao/auto-ssl/assets/4090783/e3ea47d8-7b3e-4605-94ee-689e6bb6ca45)

#### 5️⃣ 设置 GitHub Actions 权限

**路径：** `Settings` → `Actions` → `General` → `Workflow permissions`

选择：**Read and write permissions**

![Actions 权限设置](https://github.com/danbao/auto-ssl/assets/4090783/abb42eb0-fd78-4417-bf07-9cf090ee7a2c)

#### 6️⃣ 配置目标域名

编辑仓库中的 `cloudflare_domains_list.txt` 文件：
```text
example.com
*.example.com
subdomain.example.com
```
> 每行填写一个域名，支持通配符域名

#### 7️⃣ 手动触发首次运行

1. 进入 `Actions` 标签页
2. 选择对应的工作流
3. 点击「Run workflow」手动触发

## 📊 运行状态

- **证书检查**：每日 UTC 00:00 自动执行
- **续期阈值**：证书有效期小于 30 天时自动续期
- **状态报告**：详细日志记录在 `CHECK_LIST.md` 文件中

## 🔧 故障排查

### 常见问题

**Q: 证书申请失败？**
A: 请检查：
- Cloudflare API Token 权限设置
- 域名 DNS 记录是否正确
- GitHub Secrets 配置是否完整

**Q: 工作流执行失败？**
A: 请查看：
- Actions 运行日志
- 网络连接状态
- API 调用限制

### 获取支持

如遇到问题，请：
1. 查看 [Issues](../../issues) 页面
2. 提交详细的错误日志
3. 描述您的配置环境

## 📄 许可证

本项目采用开源许可证，详情请参见 [LICENSE](LICENSE) 文件。