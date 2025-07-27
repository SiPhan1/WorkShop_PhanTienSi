---
title : "Troubleshooting"
date :  "2024-12-05"
weight : 5
chapter : false
pre : "<b>5.</b>"
---

# Troubleshooting Hybrid DNS Issues

This section outlines common DNS problems in hybrid environments and how to resolve them effectively, focusing on DNS resolution failures, on-prem integration, and health check diagnostics.

---

## Common Issues and Fixes

### 1. EC2 Instances Cannot Resolve DNS

**Symptoms:**  
EC2 DNS queries return errors like `NXDOMAIN` or `SERVFAIL`.

**Possible Causes:**
- DNS support or hostname resolution is disabled in the VPC.

**Resolution:**
- Go to **VPC → Actions → Modify DNS settings**
- Ensure:
  - `Enable DNS resolution` is enabled
  - `Enable DNS hostnames` is enabled

---

### 2. On-Premise Domains Are Not Resolving

**Symptoms:**  
Internal domains (e.g., `app.internal.example.com`) cannot be resolved from VPC.

**Possible Causes:**
- Resolver endpoints not configured correctly
- Forwarding rule points to the wrong on-prem DNS IP
- Port 53 blocked by SG/NACL

**Resolution:**
- Verify **Outbound Resolver Endpoints** are in correct private subnets
- Ensure **forwarding rule** targets the correct on-prem DNS IP
- Allow UDP/TCP port 53 in **Security Groups** and **NACLs**

---

### 3. Route 53 Health Check Is Always Failing

**Symptoms:**  
Health status remains **Unhealthy**

**Possible Causes:**
- Target is not responding
- Incorrect protocol used (e.g., HTTP instead of TCP)

**Resolution:**
- Confirm endpoint is responsive
- Check **CloudWatch metrics/logs** for insights
- Ensure firewall/SG allows health check traffic

---

## Diagnostic Commands

```bash
# Query using system default resolver
dig app.internal.example.com

# Query via outbound resolver IP
dig app.internal.example.com @10.0.0.2

# Test external DNS resolution
nslookup google.com
