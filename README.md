# AWS Secure Web Infrastructure

## Project Overview

This project demonstrates how to deploy and troubleshoot a basic web server on Amazon EC2 using Amazon Linux 2023 and Apache HTTP Server.

The goal is to practice foundational AWS infrastructure, Linux administration, network access control, and web server troubleshooting.

## Architecture

- **Cloud Provider:** Amazon Web Services (AWS)
- **Compute:** Amazon EC2
- **Operating System:** Amazon Linux 2023
- **Web Server:** Apache HTTP Server (httpd)
- **Web Protocol:** HTTP
- **Access Management:** EC2 Security Groups and SSH key-based authentication
- **Region:** Asia Pacific (Sydney)

### Request Flow

```text
User's Browser
      |
      | HTTP (Port 80)
      v
AWS Security Group
      |
      v
EC2 Instance
(Amazon Linux 2023)
      |
      v
Apache HTTP Server
      |
      v
/var/www/html/index.html
      |
      v
Professional HTML/CSS Website
```

## Implementation

1. Launched an EC2 instance using Amazon Linux 2023.
2. Configured SSH access using a private key.
3. Restricted SSH inbound access to a specific public IP address.
4. Installed and started Apache HTTP Server.
5. Created a custom HTML homepage.
6. Enabled Apache to start automatically when the instance boots.
7. Verified the web server locally and through a browser.

## Troubleshooting

### Issue: HTTP 403 Forbidden

**Symptom:** The local HTTP request returned `403 Forbidden`.

**Investigation:** Checked the Apache error log at `/var/log/httpd/error_log`.

**Root cause:** Apache could not find an `index.html` file in `/var/www/html/`, and directory listing was disabled.

**Resolution:** Created `/var/www/html/index.html` with a basic HTML homepage.

**Verification:** Ran `curl -I http://localhost` and received `HTTP/1.1 200 OK`. Also verified the page in a web browser using the EC2 public IP address.

## Security Considerations

- Used SSH key-based authentication.
- Restricted SSH access to a specific public IP address.
- Allowed public HTTP access for the website.
- Reviewed inbound Security Group rules.
- Did not upload private keys or credentials to the repository.

### Inbound Security Group Rules

| Protocol | Port | Source | Purpose |
|---|---:|---|---|
| SSH | 22 | Restricted public IP (`/32`) | Secure administrative access |
| HTTP | 80 | Public internet (`0.0.0.0/0`) | Serve the public website |

**Security Notes:**
- SSH access is restricted to a specific public IP address.
- HTTP is publicly accessible so visitors can view the website.
- HTTPS/TLS is not configured in this learning project.
- Never commit private SSH keys or credentials to GitHub.

## Skills Practiced

- AWS EC2 fundamentals
- Linux command-line administration
- SSH connectivity
- Apache installation and service management
- HTTP status-code troubleshooting
- Log analysis
- Security Group configuration
- Basic HTML hosting

## Current Limitations

- The website uses HTTP and does not yet have TLS/HTTPS configured.
- This is a learning project, not a production-ready deployment.
- High availability, monitoring, automated deployment, and infrastructure as code are future improvements.

## Cost Awareness

AWS resource usage and applicable Free Plan credits should be monitored. Stop or remove resources when they are no longer needed, while considering any storage charges that may remain.

## Disclaimer

This project is for learning and portfolio demonstration purposes.
