# Security Policy

## Supported Versions

We release patches for security vulnerabilities in the following versions:

| Version | Supported          |
| ------- | ------------------ |
| Latest  | :white_check_mark: |
| < Latest| :x:                |

## Reporting a Vulnerability

We take the security of our project seriously. If you believe you have found a security vulnerability, please report it to us as described below.

### Where to Report

**Please do not report security vulnerabilities through public GitHub issues.**

Instead, please report them via one of the following methods:

1. **Email**: Send an email with details of the vulnerability to the repository maintainer
2. **GitHub Security Advisories**: Use the "Security" tab in this repository to privately report a vulnerability

### What to Include

Please include the following information in your report:

- Type of vulnerability (e.g., buffer overflow, SQL injection, cross-site scripting, etc.)
- Full paths of source file(s) related to the manifestation of the vulnerability
- The location of the affected source code (tag/branch/commit or direct URL)
- Any special configuration required to reproduce the issue
- Step-by-step instructions to reproduce the issue
- Proof-of-concept or exploit code (if possible)
- Impact of the issue, including how an attacker might exploit it

### What to Expect

After submitting a vulnerability report, you can expect:

- **Acknowledgment**: We will acknowledge receipt of your vulnerability report within 72 hours
- **Assessment**: We will assess the vulnerability and determine its severity and impact
- **Updates**: We will keep you informed about our progress toward a fix and announcement
- **Resolution**: We will notify you when the vulnerability has been fixed
- **Credit**: If you wish, we will publicly acknowledge your responsible disclosure

### Disclosure Policy

- Security issues should be disclosed responsibly
- We request that you give us reasonable time to investigate and mitigate the issue before public disclosure
- We will coordinate with you on the timing of public disclosure

## Security Best Practices

When using code or configurations from this repository:

1. **Keep Dependencies Updated**: Regularly update all dependencies to their latest secure versions
2. **Review Code**: Carefully review any code before implementing it in production environments
3. **Test in Non-Production**: Always test scripts and configurations in non-production environments first
4. **Secure Credentials**: Never commit sensitive information (passwords, API keys, tokens) to the repository
5. **Access Control**: Implement proper access controls and principle of least privilege
6. **Audit Logs**: Enable and monitor audit logging where applicable
7. **Backup**: Maintain regular backups before making configuration changes

## Security Updates

Security updates will be released as needed and announced through:

- GitHub Security Advisories
- Repository releases with security tags
- Updates to this SECURITY.md file

## Scope

This security policy applies to:

- All code in this repository
- All documentation and configuration examples
- All released versions and branches

## Additional Resources

- [GitHub Security Best Practices](https://docs.github.com/en/code-security)
- [OWASP Top Ten](https://owasp.org/www-project-top-ten/)
- [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks/)

## Contact

For non-security-related issues, please use the standard GitHub issue tracker.

Thank you for helping keep this project and its users safe!
