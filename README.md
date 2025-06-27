# Octra Wallet Generator - VPS Deployment Guide

This guide explains how to run the [`octra-labs/wallet-gen`](https://github.com/octra-labs/wallet-gen) project on a Virtual Private Server (VPS).
---

### Building from Source

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

### 3 Enable port 8888

Enable UFW:
```bash
sudo ufw enable
```
Allow incoming TCP connections on port 8888:
```bash
sudo ufw allow 8888/tcp
```
Verify the rule:
```bash
sudo ufw status verbose
```
You should see an entry like ```8888/tcp ALLOW Anywhere```

### 4. Start the server

```bash
bun start
```

### 5. Access the Web Interface

Same as above:

- Navigate to:  
  `http://<your_vps_ip_address>:8888`
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
Save the phrases and address on the safe place
---

## 📚 Resources

- 🔗 [octra-labs/wallet-gen](https://github.com/octra-labs/wallet-gen)
- 🔗 [octra-labs/node_configuration](https://github.com/octra-labs/node_configuration)

---

Happy wallet generating! 🚀
