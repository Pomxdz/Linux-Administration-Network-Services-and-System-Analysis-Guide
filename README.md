# Secure Network Programming (SNP) Project

This repository contains the documentation and scripts for a comprehensive Secure Network Programming laboratory project. The project explores the setup, configuration, and security analysis of a Linux environment using Oracle VirtualBox.

## 📄 Project Overview

The project is divided into three main pillars:
1.  **System & Network Administration:** Setting up essential services (DHCP, DNS, NTP, Web, Email).
2.  **Security & Automation:** Implementing Firewalls (iptables), SSH security, and Bash scripting.
3.  **Reverse Engineering:** Analyzing binaries using GDB to understand execution flow and encryption logic.

## 🛠️ Environment Setup

* [cite_start]**Hypervisor:** Oracle VirtualBox [cite: 22]
* [cite_start]**Host OS:** Ubuntu 24.04.2 LTS [cite: 24]
* [cite_start]**Client OS:** Kali Linux (for penetration testing and network verification) [cite: 88]
* [cite_start]**Networking:** Configured using Host-Only Adapters to simulate an isolated internal network[cite: 84].

## 🌐 Network Services Configuration

The following services were installed and configured on the Ubuntu server:

* [cite_start]**DHCP (ISC-DHCP-Server):** Configured to assign dynamic IP addresses within the `192.168.56.0/24` subnet and specific leases for clients[cite: 75, 76].
* [cite_start]**DNS (BIND9):** Configured a local master zone (`mytest.local`) to resolve hostnames to IP addresses, tested using `dig` and `nslookup`[cite: 100, 101, 109].
* [cite_start]**NTP:** Synchronized system time across the network using the Network Time Protocol[cite: 112].

## 🔒 Security & Access Control

### SSH (Secure Shell)
OpenSSH Server was configured to allow secure remote management. [cite_start]Connectivity was verified by accessing the Ubuntu server from the Kali client[cite: 154, 156].

### iptables & ACLs
Custom firewall rules were implemented to filter traffic and enforce security policies:
* [cite_start]**Blocked Sites:** Rules to reject traffic to specific IPs associated with social media platforms (Facebook, Instagram, Twitter)[cite: 163].
* [cite_start]**Port Filtering:** Blocked unencrypted HTTP traffic (Port 80) and allowed secure HTTPS traffic (Port 443)[cite: 164].

```bash
# Example Rules Implemented
sudo iptables -A OUTPUT -p tcp --dport 80 -j REJECT
sudo iptables -A OUTPUT -p tcp --dport 443 -j ACCEPT
