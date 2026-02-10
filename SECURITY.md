# Security Policy

## Reporting Security Issues

**Please do not report security vulnerabilities through public GitHub issues.**

Instead, please report security issues by emailing us at:

**security@codi.dev**

Please include as much of the following information as possible:
- Description of the vulnerability
- Steps to reproduce the issue
- Potential impact
- Suggested fix (if any)

## Response Timeline

- **Acknowledgment**: Within 48 hours
- **Initial assessment**: Within 5 business days
- **Resolution**: Varies based on severity and complexity

## Project-Specific Security Policies

This workspace manifest contains multiple projects, each with their own security considerations:

- **codi**: See `codi/SECURITY.md`
- **codi-private**: See `codi-private/SECURITY.md`
- **gitgrip**: See `gitgrip/SECURITY.md`

Please report vulnerabilities directly to the affected project's security policy when applicable.

## Security Best Practices for Contributors

- Never commit secrets, API keys, or credentials
- Use environment variables for sensitive configuration
- Follow the principle of least privilege
- Keep dependencies up to date
- Review code for security implications before submitting PRs
