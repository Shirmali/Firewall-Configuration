# 🔥 Basic Firewall Configuration & Traffic Filtering

🛡️ Project Overview

In the realm of cybersecurity, maintaining a robust defense against unauthorized access and malicious attacks begins with a well-configured firewall. Firewalls act as gatekeepers—controlling which network traffic is allowed into or out of a system based on predetermined rules. In this project, we configure a host-based firewall using UFW (Uncomplicated Firewall) on a Linux machine, reinforcing one of the foundational security layers.

This project is designed to help:

Understand firewall principles, including inbound/outbound rules and traffic filtering.

Configure UFW to protect a Linux host.

Simulate real-world scenarios using basic network testing tools like nmap and netcat.

Learn to troubleshoot why certain ports or services are blocked, open, or inaccessible.

By the end of this project, you'll have practical experience:

✅ Configuring default deny/allow policies✅ Allowing and denying specific ports and services✅ Validating firewall behavior with real testing✅ Interpreting firewall rule outputs✅ Troubleshooting common connection issues (e.g., "connection refused")

---

## 🧰 Tools & Environment

| Tool             | Purpose                        |
| ---------------- | ------------------------------ |
| **Ubuntu 22.04** | OS for firewall configuration  |
| **UFW**          | Host-based firewall            |
| **nmap**         | Port scanning                  |
| **netcat (nc)**  | Port testing tool              |
| **ss**           | View active listening services |

---

## 🪜 Step-by-Step Configuration

### 🔹 Step 1: Update & Install Dependencies

Update repositories and install necessary tools:

```bash
sudo apt update
sudo apt install ufw nmap netcat-openbsd openssh-server -y
```

---

### 🔹 Step 2: Set Default Firewall Policies

We start by blocking all incoming traffic and allowing all outgoing traffic:

```bash
sudo ufw default deny incoming
```

```bash
sudo ufw default allow outgoing
```

📸 **Screenshot:**
![Default Policy](screenshots/default_policy.png)

---

### 🔹 Step 3: Enable the Firewall

Enable UFW so all configurations take effect:

```bash
sudo ufw enable
```

📸 **Screenshot:**
![UFW Enabled](screenshots/ufw_enabled.png)

---

### 🔹 Step 4: Allow Essential Services

We allow ports for SSH, HTTP, and HTTPS:

```bash
sudo ufw allow 22    # SSH
```

```bash
sudo ufw allow 80    # HTTP
```

```bash
sudo ufw allow 443   # HTTPS
```

📸 **Screenshot:**
![Allowed Services](screenshots/allowed_services.png)

---

### 🔹 Step 5: Deny Unsecure or Unused Ports

We explicitly block FTP:

```bash
sudo ufw deny 21     # FTP
```

📸 **Screenshot:**
![Blocked FTP](screenshots/blocked_ftp.png)

---

## 🔍 Testing Firewall Rules

### ✅ Test Allowed Port (22)

```bash
nc -zv localhost 22
```

✅ Expected: *Connection succeeded* if SSH is running.

### ❌ Test Blocked Port (21)

```bash
nc -zv localhost 21
```

❌ Expected: *Connection refused*

📸 **Screenshot:**
![Test Results](screenshots/port_test_results.png)

---

## 🛠️ Troubleshooting

### Problem: "Connection Refused"

If allowed ports are still refused:

* It may be because **no service is running** on the port.
* Check active listening services:

```bash
sudo ss -tuln
```

📸 **Screenshot:**
![SS Output](screenshots/ss_output.png)

### Solution: Start the Required Service

For example, to ensure port 22 (SSH) is listening:

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

---

## 🧠 Key Takeaways

* Firewalls help enforce least privilege by controlling traffic.
* UFW simplifies iptables rules and is beginner-friendly.
* Netcat + Nmap + `ss` help verify firewall behavior.
* "Connection refused" doesn't always mean blocked—it could mean *nothing is listening*.

---

## 📚 References

* [UFW - Ubuntu Documentation](https://help.ubuntu.com/community/UFW)
* [nmap Manual](https://nmap.org/book/man.html)
* [netcat (nc)](https://linux.die.net/man/1/nc)
* [ss Command](https://linux.die.net/man/8/ss)

---

## 📂 Folder Structure

```
Firewall-Configuration/
├── README.md
└── screenshots/
    ├── default_policy.png
    ├── ufw_enabled.png
    ├── allowed_services.png
    ├── blocked_ftp.png
    ├── port_test_results.png
    └── ss_output.png
```

---


