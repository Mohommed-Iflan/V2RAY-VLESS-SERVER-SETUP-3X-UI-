# V2RAY-VLESS-SERVER-SETUP-3X-UI-
This Repository Guild you to how to create a V2RAY VLESS SERVER FREELY! and you can spoof/tunnel your network through the server

# Beginner's Guide: Setting Up an AWS VLESS-TLS Proxy Server

This guide provides a complete, step-by-step walkthrough for setting up your own secure proxy server on an AWS cloud instance using 3X-UI. It is written in simple terms so anyone—even without technical experience—can follow along.

---

## Table of Contents
1. [What You Will Need](#what-you-will-need)
2. [Step 1: Create an AWS Account & Server (EC2)](#step-1-create-an-aws-account--server-ec2)
3. [Step 2: Open Required Network Ports](#step-2-open-required-network-ports)
4. [Step 3: Connect to Your Server](#step-3-connect-to-your-server)
5. [Step 4: Automated Server Setup & Installation](#step-4-automated-server-setup--installation)
6. [Step 5: Configure Your Proxy Panel](#step-5-configure-your-proxy-panel)
7. [Step 6: Connect Your Phone or Computer](#step-6-connect-your-phone-or-computer)

---

## What You Will Need
* A computer (Windows, Mac, or Linux).
* A free **AWS (Amazon Web Services)** account.
* A mobile phone or computer to use the internet through your new proxy.

---

## Step 1: Create an AWS Account & Server (EC2)
1. Go to [aws.amazon.com](https://aws.amazon.com/) and sign up for a free account if you haven't already. [This Free Tier is only for 6 months] (you may ask for card details to verify the free tier account, but you don't charge until you upgrade to premium even the trial period end. make sure you hold 1-2 USD in your card for successful verification.)
2. Log in to the **AWS Management Console**.
3. In the search bar at the top, type **EC2** and click on the EC2 service.
4. Click on **Launch Instance**.
5. Give your server a name (e.g., `MyProxyServer`).
6. **Operating System:** Select **Ubuntu** (choose version 24.04 or latest LTS).
7. **Instance Type:** Select **t3.micro** (this is usually covered under the AWS Free Tier).
8. **Key Pair:** Click *Create new key pair*, name it something simple like `my-key`, download it, and save it somewhere safe on your computer.
9. Click the orange **Launch Instance** button on the right.

---

## Step 2: Open Required Network Ports
Before your server can talk to the outside world, you need to open specific doors (ports) in the AWS firewall:
1. From your EC2 Dashboard, click on your running instance, then click on the **Security** tab at the bottom.
2. Click on your **Security Group** link (starts with `sg-...`).
3. Click **Edit inbound rules**.
4. Add the following three rules:
   * **Rule 1:** Type: `SSH` | Port: `22` | Source: `Anywhere-IPv4 (0.0.0.0/0)`
   * **Rule 2:** Type: `Custom TCP` | Port Range: `443` | Source: `Anywhere-IPv4 (0.0.0.0/0)`
   * **Rule 3:** Type: `Custom TCP` | Port Range: `2053` | Source: `Anywhere-IPv4 (0.0.0.0/0)`
5. Click **Save rules**.
6. Go back to your Instance summary, look for **Source / destination check**, click *Actions > Networking*, and **Stop / Disable** it.
<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/d79a2b03-927b-4b2b-a55e-041fafd2a058" />

---

## Step 3: Connect to Your Server
1. Find your server's **Public IPv4 address** on your EC2 instance dashboard (it looks like `3.x.x.x`, You can easily find in instances page it named like "Public IPv4 address").
3. Open your computer's terminal (Command Prompt on Windows, or Terminal on Mac/Linux).
4. Connect to your server using SSH by typing: (Replace you actual `Public IPv4 address` with `YOUR_SERVER_IP` & Replace the `path/to/my-key.pem` your actual key downloaded path make sure keep the quates with it `" "`)

   ```bash
   ssh -i "path/to/my-key.pem" ubuntu@YOUR_SERVER_IP

---

## Step 4: Automated Server Setup & Installation
Once you are logged into your server terminal, run these commands one by one:

1. Give the root access

```bash
   sudo -i
```
```bash
   apt update && apt install -y curl wget openssl
```
```bash
   mkdir -p /etc/x-ui
```
2. This is a SSL Certificate created for `youtube.com`
```bash
  openssl req -x509 -newkey rsa:2048 -keyout /etc/x-ui/server.key -out /etc/x-ui/server.crt -days 3650 -nodes -subj "/CN=youtube.com"
```
```bash
   chmod 644 /etc/x-ui/server.crt
```
```bash
   chmod 600 /etc/x-ui/server.key
```
3. Install 3X-UI
```bash
   bash <(curl -Ls [https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh](https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh))
```
if prompted select the options like in image 
<img width="1114" height="590" alt="image" src="https://github.com/user-attachments/assets/fcc5f6e2-4faf-42cd-97cd-d6a8103dda10" />

3. After that Scroll up along in command prompt you can see all the details of your panel is showing up in there, copy the access link and paste it in the browser.
<img width="1114" height="267" alt="image" src="https://github.com/user-attachments/assets/44151dc6-2412-4ba5-9c10-05416e828d13" />
then use the username password to login to the panel
<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/c031ce4d-b189-483c-8c1f-694bcc0b2ff2" />

5. 
```bash
   apt update && apt install -y curl wget openssl
```
```bash
   apt update && apt install -y curl wget openssl
```
