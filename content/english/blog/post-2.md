---
title: "Connect to your server via SSH: A Guide to SSH and Public Key Authentication"
meta_title: ""
description: "this is meta description"
date: 2023-07-07T05:00:00Z
image: "/images/blog/ssh1.png"
categories: ["Internet", "Cloud"]
author: "Yuhang"
tags: ["technology", "ssh"]
draft: false
---

# Introduction

Secure Shell (SSH) is an indispensable cryptographic protocol designed to facilitate secure communications over an untrusted network. Widely adopted for tasks such as remote server administration, secure file transfers, and various other network services, SSH is a cornerstone of modern cybersecurity. One of its most compelling features is the use of cryptographic key pairs for authentication, offering a far more secure alternative to traditional password-based logins. This blog post serves as a comprehensive guide to setting up and optimizing SSH with public key authentication.

## Checking and Installing SSH on Your Machine: A Prerequisite for Security

Before you can embark on the journey of secure and efficient remote server management, it's imperative to ensure that SSH is installed on both your local and remote machines. Here's how you can verify its presence and install it if necessary:

### Verifying SSH Installation

**On UNIX-based Systems (Linux/Mac):**

1. Launch a terminal window.
2. Execute the command `which ssh`.
3. If SSH is installed, the terminal will return the installation path. If not, there will be no output.

**On Windows:**

1. Open either PowerShell or Command Prompt.
2. Input `ssh` and hit Enter.
3. If SSH is installed, usage instructions will appear. Otherwise, an error message will be displayed.

### Installation Guide

**On Linux:**

1. Open a terminal.
2. Update the package lists with `sudo apt update`.
3. Install SSH using `sudo apt install openssh-server`.

**On Windows:**

1. Navigate to Settings > Apps > Optional Features.
2. Scroll down and select "Add a feature."
3. Search for "SSH Client" and click on "Install."

Note: SSH comes pre-installed on macOS, eliminating the need for separate installation.

## Disabling Password Authentication: A Security Imperative

Before delving into the realm of key-based authentication, it's crucial to comprehend the vulnerabilities associated with password-based logins, such as susceptibility to brute-force attacks and phishing schemes. To fortify your server against these threats, disabling password authentication is advisable.

### Steps to Disable Password Authentication

1. Access the SSH configuration file using `vim /etc/ssh/sshd_config`.
2. Locate the `PasswordAuthentication` parameter and set it to `no`.

**Advantages and Risks**

**Advantages:**

- Enhanced resilience against brute-force attacks.
- Minimized risk of unauthorized access.

**Risks:**

- Losing your private key will result in losing access to the server.

## Configuring SSH: Tailoring Your Security

The SSH configuration file, commonly known as `ssh_config`, offers a plethora of settings that can be customized to streamline the login process and bolster security measures.

### Tips for Configuration

- Specify the `IdentityFile` to direct SSH to your private key, especially useful when managing multiple keys.
- Include `IdentitiesOnly yes` to restrict SSH connections to use only the designated identity file.

## Uploading the Public Key: A Step-by-Step Guide

After generating your SSH key pair, the subsequent step involves uploading your public key to the server. This can be accomplished manually with a series of straightforward commands.

### Commands for Uploading Public Key

1. Display your public key with `cat ~/.ssh/id_rsa.pub`.
2. Log into your server and execute the following commands: `mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys`
3. Set the appropriate permissions: `chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys`
4. Append your public key to the server's `authorized_keys` file.

## Managing Private Key Permissions: A Security Must-Have

Incorrect permissions on your private key file can be a gaping security hole. It's imperative to set the correct permissions to mitigate this risk.

### How to Set Permissions

**On Linux:**

Use `sudo chmod 600 private_key_location`.

**On Windows 10:**

Right-click on the key file, navigate to Properties > Security > Advanced > Disable Inheritance > Convert. Remove all users except the owner of the key.

## Generating a Robust SSH Key Pair on Linux

To generate a secure SSH key pair on Linux, use the following command: `ssh-keygen -t rsa -b 2048`

This command will produce a 2048-bit RSA key pair, providing a high level of security.

## Specifying an SSH Port: Flexibility and Security

SSH typically operates on port 22, but you have the flexibility to specify a different port if required.

### Command to Specify Port

Use `ssh username@server_name_or_IPaddr -p port_number` to connect.

## Customizing the SSH Configuration File: Advanced Security Measures

For those looking to further enhance security, the SSH configuration file can be modified to disable all password-based authentication.

### Commands for Customization

Open the SSH configuration file with `vim /etc/ssh/sshd_config`.

Change `PermitRootLogin yes` to `PermitRootLogin prohibit-password`.

## Utilizing AWS-Generated Key Pairs: A Convenient Option

If you're an AWS user, the platform will automatically generate a .pem key file for you. All you need to do is adjust the permissions of the key file and use it like any standard private key.

## Conclusion

Mastering SSH and public key authentication is indispensable for anyone engaged in server management or secure communications. By understanding how to disable password-based authentication, fine-tune SSH configurations, manage key permissions, and leverage AWS-generated keys, you can significantly elevate the security and efficiency of your operations.
