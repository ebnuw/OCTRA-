## Wallet-Gen VPS Deployment Guide

This guide will walk you through setting up and running the [octra-labs/wallet-gen](https://github.com/octra-labs/wallet-gen) project on a VPS. At the end, you'll have a `wallet-gen-setup.md` file ready to upload to GitHub.

---

### Table of Contents

1. [Prerequisites](#prerequisites)
2. [Server Setup](#server-setup)
3. [Cloning the Repository](#cloning-the-repository)
4. [Environment Configuration](#environment-configuration)
5. [Installing Dependencies](#installing-dependencies)
6. [Installing Bun](#installing-bun)
7. [Running the Application](#running-the-application)
8. [Verification](#verification)
9. [Automating Startup](#automating-startup)
10. [Security Considerations](#security-considerations)
11. [Uploading the Markdown File](#uploading-the-markdown-file)

---

## Prerequisites

- A VPS instance (e.g., Ubuntu 22.04 LTS) with root or sudo access
- Domain name or public IP for access
- SSH client
- Basic knowledge of Linux commands

---

## 1. Server Setup

1. **Connect via SSH**

   ```bash
   ssh username@your_vps_ip
   ```

2. **Update packages**

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

3. **Install utilities** (Git, curl, build-essential)

   ```bash
   sudo apt install -y git curl build-essential
   ```

---

## 2. Cloning the Repository

1. **Navigate to home**

   ```bash
   cd ~
   ```

2. **Clone **``

   ```bash
   git clone https://github.com/octra-labs/wallet-gen.git
   cd wallet-gen
   ```

---

## 3. Environment Configuration

1. **Copy example env file**

   ```bash
   cp .env.example .env
   ```

2. **Edit **``

   ```bash
   nano .env
   ```

   - Set `RPC_URL`, `PRIVATE_KEY`, and any other required variables.

3. **Save and exit** (`Ctrl+O`, `Enter`, `Ctrl+X`)

---

## 4. Installing Dependencies

1. **Install Node.js** (v16+ recommended)

   ```bash
   curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
   sudo apt install -y nodejs
   ```

2. **Verify Node.js and npm**

   ```bash
   node -v && npm -v
   ```

3. **Install project dependencies**

   ```bash
   npm install
   ```

---

## 5. Installing Bun

The `wallet-gen` project uses [Bun](https://bun.sh), a fast JavaScript runtime. You need to install it first.

1. **Install Bun**

   ```bash
   curl -fsSL https://bun.sh/install | bash
   ```

2. **Reload shell config**

   ```bash
   source ~/.bashrc  # or source ~/.zshrc if you use Zsh
   ```

3. **Verify Bun installation**

   ```bash
   bun -v
   ```

---

## 6. Running the Application

1. **Development mode**

   ```bash
   bun dev
   ```

2. **Production build and start**

   ```bash
   bun build --compile --outfile=wallet-generator ./wallet_generator.ts
   bun wallet_generator.ts
   ```

---

## 7. Verification

Open your browser and navigate to `http://your_vps_ip:3000` or your domain to verify the wallet generator is operational.

---

## 8. Automating Startup

1. **Create a systemd service** (`/etc/systemd/system/wallet-gen.service`):

   ```ini
   [Unit]
   Description=Wallet-Gen Service
   After=network.target

   [Service]
   WorkingDirectory=/home/username/wallet-gen
   ExecStart=/root/.bun/bin/bun wallet_generator.ts
   Restart=always
   User=username
   Environment=NODE_ENV=production
   EnvironmentFile=/home/username/wallet-gen/.env

   [Install]
   WantedBy=multi-user.target
   ```

2. **Enable and start service**

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable wallet-gen
   sudo systemctl start wallet-gen
   ```

3. **Check status**

   ```bash
   sudo systemctl status wallet-gen
   ```

---

## 9. Security Considerations

- Use a firewall (e.g., `ufw`) to restrict unused ports.
- Store environment secrets securely (consider vault solutions).
- Regularly update OS and dependencies.

---

## 10. Uploading the Markdown File

After customizing this guide, save it as `wallet-gen-setup.md` in your repository root:

```bash
cp /home/username/wallet-gen-setup.md /home/username/wallet-gen/
cd wallet-gen
git add wallet-gen-setup.md
git commit -m "Add VPS deployment guide"
git push origin main
```

---

With this, your `wallet-gen-setup.md` is live on GitHub, making it easy for others to deploy the project on a VPS.

