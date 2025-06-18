# 🔥 Basic Firewall Configuration & Traffic Filtering

## 📌 Project Overview

This project demonstrates how to configure a host-based firewall using **UFW (Uncomplicated Firewall)** on a Linux system. It includes setting default security policies, adding allow/deny rules, and validating firewall behavior using tools like `nmap` and `netcat`. It's an essential skill in any cybersecurity role to understand traffic control and reduce the attack surface of a system.

---

## 🛠️ Tools & Technologies

- **OS:** Ubuntu 22.04 LTS (or Debian-based Linux)
- **Firewall:** UFW (Uncomplicated Firewall)
- **Testing Tools:**
  - `nmap` – for port scanning
  - `netcat (nc)` – for basic connectivity testing

---

## 🧱 Firewall Configuration Steps

### 1. Install Required Tools
```bash
sudo apt update
sudo apt install ufw nmap netcat-openbsd -y
---

✅ Note: Used netcat-openbsd instead of netcat to avoid the "no installation candidate" error.

# Step 2: Set Default Policies
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Step 3: Enable UFW
sudo ufw enable

# Step 4: Allow Essential Services
sudo ufw allow 22    # SSH
sudo ufw allow 80    # HTTP
sudo ufw allow 443   # HTTPS

# Step 5: Deny Unsecure/Unused Ports
sudo ufw deny 21     # Block FTP

