---
title: "Complete Guide: Securing SSH and Using Private Keys on Linux"
date: 2026-03-04
draft: false
categories: ["Linux", "Security"]
tags: ["ssh", "linux", "security", "private-keys", "hardening", "sysadmin"]
author: gnolasco
---

Secure Shell (SSH) is the standard protocol for remotely managing Linux systems. While password authentication works, it is significantly less secure than key-based authentication. Using SSH private keys improves security, prevents brute-force attacks, and enables safer automation for administrators.

This guide walks through generating SSH keys, configuring servers for key-based authentication, and applying SSH hardening best practices.

## Prerequisites
- A Linux client machine
- Access to a remote Linux server
- A user account with `sudo` privileges on the server
- OpenSSH installed (default on most Linux systems)

# 1. Generate an SSH Key Pair

SSH authentication uses a **public/private key pair**.

- **Private key** → stays on your local machine and must never be shared
- **Public key** → stored on the remote server

Generate a modern SSH key:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

# ... (remaining content omitted for brevity)