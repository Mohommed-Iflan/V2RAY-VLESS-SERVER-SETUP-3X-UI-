# V2RAY-VLESS-SERVER-SETUP-3X-UI-
This Repository Guild you to how to create a V2RAY VLESS SERVER FREELY! and you can spoof/tunnel your network through the server

# AWS VLESS-TLS Proxy Server with 3X-UI

A comprehensive guide and automated setup script for deploying a high-performance VLESS + TCP + TLS proxy server on an AWS EC2 instance using 3X-UI. Designed for optimizing data packages (such as YouTube-specific unlimited bundles) and ensuring seamless proxy routing.

---

## Features
* **Lightweight & Efficient:** Runs smoothly on AWS free-tier instances (`t3.micro`).
* **Secure TLS Encryption:** Uses custom domain SNI masking (`youtube.com`).
* **Easy Management:** Powered by the intuitive 3X-UI web dashboard.
* **Automated Setup:** Includes quick scripts for certificate generation and dependency configuration.

---

## Prerequisites
* An active **AWS Account** with EC2 access.
* A client proxy app (e.g., **v2rayNG** for Android, **Hiddify**, or v2rayN for desktop).

---

## Step 1: AWS EC2 Instance Setup
1. Launch a new EC2 instance (recommended: **Ubuntu 24.04** or **Amazon Linux 2023**, `t3.micro`).
2. Configure **Security Groups** to allow inbound traffic on the following ports:
   * **TCP 443** (Proxy traffic)
   * **TCP 2053** (3X-UI Web Panel)
   * **TCP 22** (SSH access)
3. Select your instance in the EC2 console, go to **Actions > Networking**, and ensure **Source/Destination Check** is **Disabled**.

---

## Step 2: Automated Server Configuration & Installation
Connect to your AWS instance via SSH, switch to root, and run the following automated setup script to install dependencies and generate the required TLS certificates:

```bash
sudo -i
# Update system packages
apt update && apt install -y curl wget openssl

# Generate SSL certificates for VLESS-TLS
mkdir -p /etc/x-ui
openssl req -x509 -newkey rsa:2048 -keyout /etc/x-ui/server.key -out /etc/x-ui/server.crt -days 3650 -nodes -subj "/CN=youtube.com"
chmod 644 /etc/x-ui/server.crt
chmod 600 /etc/x-ui/server.key

# Install 3X-UI panel
bash <(curl -Ls [https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh](https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh))
