# Secure Network Programming (SNP) Project

This repository contains the documentation and scripts for a comprehensive Secure Network Programming laboratory project. The project explores the setup, configuration, and security analysis of a Linux environment using Oracle VirtualBox.

## 📄 Project Overview

The project is divided into three main pillars:
1.  **System & Network Administration:** Setting up essential services (DHCP, DNS, NTP, Web, Email).
2.  **Security & Automation:** Implementing Firewalls (iptables), SSH security, and Bash scripting.
3.  **Reverse Engineering:** Analyzing binaries using GDB to understand execution flow and encryption logic.

## 🛠️ Environment Setup

* **Hypervisor:** Oracle VirtualBox.
* **Host OS:** Ubuntu 24.04.2 LTS. 
* **Client OS:** Kali Linux (for penetration testing and network verification)
* **Networking:** Configured using Host-Only Adapters to simulate an isolated internal network.

## 🌐 Network Services Configuration

The following services were installed and configured on the Ubuntu server:

* **DHCP (ISC-DHCP-Server):** Configured to assign dynamic IP addresses within the `192.168.56.0/24` subnet and specific leases for clients.
* **DNS (BIND9):** Configured a local master zone (`mytest.local`) to resolve hostnames to IP addresses, tested using `dig` and `nslookup`.
* **NTP:** Synchronized system time across the network using the Network Time Protocol.

## 🔒 Security & Access Control

### SSH (Secure Shell)
OpenSSH Server was configured to allow secure remote management. Connectivity was verified by accessing the Ubuntu server from the Kali client.

### iptables & ACLs
Custom firewall rules were implemented to filter traffic and enforce security policies:
* **Blocked Sites:** Rules to reject traffic to specific IPs associated with social media platforms (Facebook, Instagram, Twitter).
* **Port Filtering:** Blocked unencrypted HTTP traffic (Port 80) and allowed secure HTTPS traffic (Port 443).

## ⚙️ Automation
A custom Bash script (log_cleanup.sh) was created to automate system maintenance.

### Features:
Creates log and backup directories.
Deletes logs older than 7 days.
Archives remaining logs into a .tar.gz file stamped with the current date.
Scheduled via Cron Job to run automatically every Sunday at midnight (0 0 * * 0).

## 🕵️ Reverse Engineering & Debugging with GDB
This module involved analyzing an unknown executable file to understand its internal logic.

### Process:
**Architecture Check:** Determined the binary was x86_64 using uname -m.
**Execution:** The program accepts an input (Student IT Number) and generates a data.txt file containing encrypted content .
**Debugging (GDB):**
Analyzed functions using info functions to reveal a custom function: xor_encrypt_decrypt.
Disassembled the code (Intel flavor) to trace memory and register values.
Identified that the program uses a specific key to XOR encrypt an input string.
Verification: Validated that the data.txt file contained the XOR-encrypted result of the discovered value.
