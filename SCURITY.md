# Security Policy

## 🔒 Reporting Security Vulnerabilities

We take security seriously and appreciate your efforts to responsibly disclose your findings. If you discover a security vulnerability, please follow these guidelines:

### 📧 How to Report

**DO NOT report security vulnerabilities through public GitHub issues, discussions, or pull requests.**

Instead, please report vulnerabilities through one of these secure channels:

1. **GitHub Security Advisories** (Preferred)
   - Navigate to the repository's Security tab
   - Click "Report a vulnerability"
   - Fill out the private vulnerability report form

2. **Email**
   - Send details to: `security@[your-domain].com`
   - Use PGP encryption if possible (key available on request)

3. **Security Contact Form**
   - Visit: `https://[your-website]/security-report`

### 📋 What to Include in Your Report

To help us triage and fix the issue quickly, please include:

- **Description**: Clear explanation of the vulnerability
- **Impact**: Potential security impact and attack scenarios
- **Reproduction Steps**: Detailed steps to reproduce the issue
- **Affected Components**: Specific files, functions, or modules affected
- **Version Information**: Software version, OS, and environment details
- **Proof of Concept**: Code, screenshots, or videos (if applicable)
- **Suggested Fix**: Your recommendations for remediation (optional)
- **CVE Request**: Whether you'd like to request a CVE identifier

### ⏱️ Response Timeline

We are committed to addressing security issues promptly:

| Timeline | Action |
|----------|--------|
| **24-48 hours** | Initial acknowledgment of your report |
| **3-5 business days** | Preliminary assessment and severity rating |
| **7-14 days** | Detailed response with remediation plan |
| **30-90 days** | Patch development and coordinated disclosure |

**Note**: Timeline may vary based on complexity and severity.

### 🎖️ Recognition

We value security researchers who help keep our project safe:

- Security advisories will credit reporters (unless anonymity is requested)
- Critical findings may be featured in release notes
- Researchers will be notified before public disclosure
- Hall of Fame listing on our security page (with permission)

---

## 🛡️ Supported Versions

We actively maintain security updates for the following versions:

| Version | Supported | End of Life |
|---------|-----------|-------------|
| 2.x.x   | ✅ Yes    | TBD         |
| 1.5.x   | ✅ Yes    | Dec 2025    |
| 1.0-1.4 | ⚠️ Limited | Jun 2025  |
| < 1.0   | ❌ No     | Ended       |

**Legend:**
- ✅ **Full Support**: Active security patches and updates
- ⚠️ **Limited Support**: Critical security fixes only
- ❌ **No Support**: No longer maintained

### Migration Guidance

If you're using an unsupported version, please upgrade:
- Follow our [upgrade guide](./UPGRADING.md)
- Review [breaking changes](./CHANGELOG.md)
- Contact support for enterprise migration assistance