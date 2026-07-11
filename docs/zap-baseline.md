# OWASP ZAP Baseline Scan

## Overview

The OWASP ZAP Baseline Scan is a lightweight Dynamic Application Security Testing (DAST) approach designed to identify common web application security issues without actively exploiting the target application.

Unlike an Active Scan, the Baseline Scan focuses primarily on passive analysis, making it suitable for integration into Continuous Integration and Continuous Delivery (CI/CD) pipelines.

This document explains how the Baseline Scan works, its advantages, limitations, and how it is used within this laboratory.

---

# What is DAST?

Dynamic Application Security Testing (DAST) is a black-box security testing methodology that evaluates a running application from the perspective of an external user.

Unlike Static Application Security Testing (SAST), DAST does not require access to the application's source code.

Instead, it interacts with the application over HTTP or HTTPS, observing requests and responses to identify potential security vulnerabilities.

Typical findings include:

- Missing security headers
- Information disclosure
- Cookie configuration issues
- Cross-Site Scripting (XSS)
- SQL Injection
- Directory listing
- Server misconfiguration
- Authentication weaknesses

---

# Why OWASP ZAP?

OWASP Zed Attack Proxy (ZAP) is one of the most widely used open-source web application security testing tools.

It is maintained by the Open Worldwide Application Security Project (OWASP) and supports both manual penetration testing and automated security scanning.

Key features include:

- Passive scanning
- Active scanning
- Spidering
- API testing
- Authentication support
- Automation Framework
- Docker images
- REST API
- HTML, XML, JSON and SARIF reporting

Because of these capabilities, OWASP ZAP is commonly integrated into DevSecOps pipelines.

---

# What is a Baseline Scan?

The Baseline Scan is a safe and non-intrusive security assessment.

It crawls the target application and performs passive analysis without launching attack payloads against the application.

The scan is designed to detect common security weaknesses while minimizing the risk of affecting the application's behavior.

This makes it an excellent choice for automated execution during software development.

---

# How the Baseline Scan Works

The Baseline Scan follows several phases.

```text
Target URL

↓

Spider

↓

Collect HTTP Requests

↓

Passive Analysis

↓

Security Rules

↓

Generate HTML Report
```

---

## Phase 1 – Spidering

The spider automatically explores the application.

It discovers:

- Pages
- Links
- Forms
- Static resources
- Endpoints

The collected URLs become the input for the passive analysis phase.

---

## Phase 2 – Passive Analysis

During passive analysis, OWASP ZAP inspects all HTTP traffic exchanged between the client and the application.

Unlike Active Scanning, no malicious payloads are sent.

Examples of passive checks include:

- Missing HTTP Security Headers
- Cookie Flags
- Information Disclosure
- Content Type Issues
- Server Version Disclosure
- Cache Control Problems

---

## Phase 3 – Report Generation

After processing all observed traffic, OWASP ZAP generates an HTML report summarizing the identified findings.

The report includes:

- Alert name
- Risk level
- Confidence
- Description
- Affected URL
- Recommendation
- References

---

# Passive Scan vs Active Scan

| Feature | Passive Scan | Active Scan |
|----------|--------------|-------------|
| Sends attack payloads | No | Yes |
| Safe for production | Usually Yes | Usually No |
| Modifies application state | No | Possible |
| Fast execution | Yes | No |
| CI/CD Friendly | Yes | Sometimes |
| Detects deep vulnerabilities | Limited | Better |

---

# Baseline Scan vs Full Scan

| Feature | Baseline Scan | Full Scan |
|----------|---------------|-----------|
| Spider | Yes | Yes |
| Passive Rules | Yes | Yes |
| Active Rules | No | Yes |
| Safe for Production | Generally Yes | Not Recommended |
| Typical Runtime | Minutes | Longer |
| CI/CD Integration | Excellent | Better suited to staging environments |

---

# Baseline Scan vs API Scan

| Feature | Baseline Scan | API Scan |
|----------|---------------|----------|
| Target | Web Application | REST / SOAP / GraphQL APIs |
| Crawling | Spider | API Definition |
| Input | URLs | OpenAPI, SOAP or GraphQL specification |
| Typical Usage | Websites | Web Services |

---

# Risk Levels

OWASP ZAP categorizes findings according to their potential impact.

| Risk | Meaning |
|------|---------|
| Informational | No vulnerability detected, but useful information was collected. |
| Low | Minor security issue with limited impact. |
| Medium | Security weakness that should be addressed. |
| High | Significant vulnerability requiring immediate attention. |

---

# Advantages

The Baseline Scan offers several benefits.

- Safe automation
- Fast execution
- No source code required
- Easy Docker integration
- CI/CD friendly
- HTML report generation
- Suitable for security awareness and training

---

# Limitations

The Baseline Scan also has important limitations.

- Does not perform active exploitation.
- May miss vulnerabilities requiring authentication.
- Limited coverage of complex workflows.
- Does not replace manual penetration testing.
- Does not replace secure code reviews.
- Limited detection of business logic flaws.

For comprehensive security testing, additional approaches such as Active Scans, SAST, SCA, and manual penetration testing should be considered.

---

# Integration in This Laboratory

Within this project, the Baseline Scan is executed automatically through GitHub Actions.

The workflow performs the following sequence:

```text
Start DVWA

↓

Verify Application

↓

Run OWASP ZAP Baseline Scan

↓

Generate HTML Report

↓

Upload Report as Artifact
```

This demonstrates how DAST can be integrated into a DevSecOps workflow using containerized infrastructure and continuous integration.

---

# Learning Objectives

After completing this laboratory, you should understand:

- What DAST is.
- How OWASP ZAP performs passive analysis.
- Differences between Baseline, Full, and API Scans.
- How DAST integrates into CI/CD.
- How to interpret an OWASP ZAP report.
- The strengths and limitations of automated security testing.

---

# References

- OWASP ZAP Documentation
- OWASP Top 10
- OWASP Testing Guide
- OWASP ASVS
- NIST Secure Software Development Framework (SSDF)
