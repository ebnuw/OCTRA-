# Octra Wallet Generator - VPS Deployment Guide

This guide explains how to run the [`octra-labs/wallet-gen`](https://github.com/octra-labs/wallet-gen) project on a Virtual Private Server (VPS). You have two primary options:

- Use a **pre-built executable** (recommended for ease of use)
- **Build from source** (for customization or development)

---

## 🚀 Option 1: Using a Pre-built Executable (Recommended)

This is the fastest way to get started.

### 1. Download the binary

- Visit the [Releases page](https://github.com/octra-labs/wallet-gen/releases).
- Download `wallet-generator-linux-x64.tar.gz`.

### 2. Deploy to your VPS

Connect to your VPS using SSH and follow these steps:

```bash
# Upload the file (use scp or SFTP)
scp wallet-generator-linux-x64.tar.gz user@your_vps_ip:~

# Connect to your VPS
ssh user@your_vps_ip

# Extract the archive
tar -xzf wallet-generator-linux-x64.tar.gz

# Make the binary executable
chmod +x wallet-generator

# Run the wallet generator
./wallet-generator
```

### 3. Access the Web Interface

- Open your browser and go to:  
  `http://<your_vps_ip_address>:8888`

> ⚠️ **Firewall Note:** Make sure port `8888` is open on your VPS.

---

## 🔧 Option 2: Building from Source

Use this option if you want to modify the code or build the latest version.

### 1. Install Bun on your VPS

```bash
curl -fsSL https://bun.sh/install | bash
source ~/.bashrc  # or restart shell
bun --version
```

### 2. Clone and install dependencies

```bash
git clone https://github.com/octra-labs/wallet-gen.git
cd wallet-gen
bun install
```

### 3. Start the server

```bash
# Run normally
bun start

# Or, for development (with hot reload)
bun dev
```

### 4. Access the Web Interface

Same as above:

- Navigate to:  
  `http://<your_vps_ip_address>:8888`

> ⚠️ **Note:** Open port `8888` in your VPS firewall settings.

---

## 🪙 Generating Wallets

Once the interface is open in your browser:

- Click **"GENERATE NEW WALLET"**
- View:
  - Mnemonic phrase
  - Private & public keys
  - Address
  - Test signature
  - Address derivation for different networks

Wallets are **automatically saved** to your VPS disk.

---

## 📚 Resources

- 🔗 [octra-labs/wallet-gen](https://github.com/octra-labs/wallet-gen)
- 🔗 [octra-labs/node_configuration](https://github.com/octra-labs/node_configuration)

---

Happy wallet generating! 🚀
