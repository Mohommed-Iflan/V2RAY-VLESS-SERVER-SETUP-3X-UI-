# GUILD: V2RAY-VLESS-SERVER-SETUP-3X-UI
* This Repository Guild you to how to create a V2RAY VLESS SERVER FREELY! and you can spoof/tunnel your network through the server. This guide provides a complete, step-by-step walkthrough for setting up your own secure proxy server on an AWS cloud instance using 3X-UI. It is written in simple terms so anyone—even without technical experience—can follow along.
--
> [!WARNING]
> ### ⚠️ Usage Policy & Credits
> **Everyone is permitted to utilize this resource, and it must not be sold to others. This is intended solely for personal use. This approach will ensure that technology remains accessible to all and fosters the development of an organic technology community.**

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

## Now you successfully completed the setup, so you can add inbound that fits you! 
### EXTRA - I created an inbound for `Airtel YouTube Unlimited 260/=`
1. Click on Inbounds
2. Click on General Actions
3. Then click on `Import an Inbound`
4. Copy and paste this JSON
```bash
  {
  "id": 1,
  "userId": 0,
  "up": 13405416640,
  "down": 34734063179,
  "total": 0,
  "remark": "YOUTUBE-V2RAY",
  "enable": true,
  "expiryTime": 0,
  "trafficReset": "never",
  "trafficResetDay": 1,
  "lastTrafficResetTime": 0,
  "listen": "",
  "port": 443,
  "protocol": "vless",
  "settings": {
    "clients": [
      {
        "auth": "laiq8wezox6o2h47",
        "comment": "",
        "created_at": 1788695470589,
        "email": "ADMIN",
        "enable": true,
        "expiryTime": 0,
        "id": "fc10bc82-109c-4ffb-840b-87b1e726fcdc",
        "limitIp": 0,
        "password": "58dnafdef36mwtom",
        "reset": 0,
        "resetDay": 0,
        "resetMax": 0,
        "security": "auto",
        "subId": "nex400uj1op2cfzv",
        "tgId": 0,
        "totalGB": 0,
        "trafficReset": "never",
        "trafficResetDay": 1,
        "updated_at": 1789363344000
      }
    ],
    "decryption": "none",
    "encryption": "none"
  },
  "streamSettings": {
    "network": "tcp",
    "tcpSettings": {
      "acceptProxyProtocol": false,
      "header": {
        "type": "none"
      }
    },
    "security": "tls",
    "tlsSettings": {
      "serverName": "youtube.com",
      "minVersion": "1.2",
      "maxVersion": "1.3",
      "cipherSuites": "",
      "rejectUnknownSni": false,
      "disableSystemRoot": false,
      "enableSessionResumption": false,
      "certificates": [
        {
          "certificateFile": "/etc/x-ui/server.crt",
          "keyFile": "/etc/x-ui/server.key",
          "ocspStapling": 0,
          "oneTimeLoading": false,
          "usage": "encipherment",
          "buildChain": false
        }
      ],
      "alpn": [
        "h2",
        "http/1.1"
      ],
      "echServerKeys": "",
      "settings": {
        "fingerprint": "chrome",
        "echConfigList": "",
        "pinnedPeerCertSha256": [],
        "verifyPeerCertByName": ""
      }
    }
  },
  "tag": "in-443-tcp",
  "sniffing": {
    "enabled": true,
    "destOverride": [
      "http",
      "tls",
      "quic",
      "fakedns"
    ]
  },
  "clientStats": [
    {
      "id": 3,
      "inboundId": 1,
      "enable": true,
      "email": "ADMIN",
      "uuid": "fc10bc82-109c-4ffb-840b-87b1e726fcdc",
      "subId": "nex400uj1op2cfzv",
      "up": 13340867918,
      "down": 34669730741,
      "expiryTime": 0,
      "total": 0,
      "reset": 0,
      "resetDay": 0,
      "resetMax": 0,
      "resetCount": 0,
      "lastOnline": 1789376880002,
      "lastSubFetch": 0
    }
  ],
  "nodeId": null,
  "shareAddrStrategy": "listen",
  "shareAddr": "",
  "subSortIndex": 1,
  "disableFlow": false,
  "originNodeGuid": "",
  "fallbackParent": null
}
```
5. then click import
6. Click on 3 dots - Export All URLS
7. Copy the URL and import it in your client app (eg.NetMod)

> [!IMPORTANT]
> **If you're using different mobile plans, it would be great to explore all the inbound options to ensure everything works smoothly by adjusting the inbound settings. Perhaps you could take some time to research this and kindly share your findings in the comments below with your successful inbound setup—it would be incredibly helpful for others! Thank you!**

---
