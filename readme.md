# ☀️ Nexus III CLI Setup Guide

> Translated from https://github.com/HerculesNode/Testnet-Rehber/tree/main/Nexus

## ✅ Prerequisites

- Ubuntu 20.04 / 22.04 / 24.04  
- Docker (optional, recommended)  
- Minimum 8 GB RAM (16 GB preferred)  
- Stable internet connection  

## 🧱 Step 1: Prepare Environment

```bash
mkdir nexus
cd nexus
```

## 🐳 Step 2: Create Dockerfile

Create a file named `Dockerfile` with the following content:

```Dockerfile
FROM ubuntu:24.04

RUN apt update && apt install -y curl bash libssl-dev ca-certificates

RUN curl https://cli.nexus.xyz/ | sh

ENV PATH="/root/.nexus/bin:$PATH"

CMD ["/bin/bash"]
```

## 🛠 Step 3: Build and Run Docker Container

### For Ubuntu 24.04:

```bash
docker build -t nexus-debug .
docker run -it --rm nexus-debug
```

### For Ubuntu 22.04 or Network Issues:

```bash
sudo nano /etc/docker/daemon.json
```

Paste:

```json
{
  "dns": ["8.8.8.8", "8.8.4.4"]
}
```

Restart Docker:

```bash
sudo systemctl restart docker
```

Then:

```bash
docker build --network=host -t nexus-debug .
docker run -it --rm nexus-debug
```

## 📦 Step 4: Install Nexus CLI

Inside the container or local machine:

```bash
curl https://cli.nexus.xyz/ | sh
source /root/.profile
```

## 🆔 Step 5: Get Your Node ID

Visit [https://app.nexus.xyz/nodes](https://app.nexus.xyz/nodes) and copy your **Node ID**.

## 🚀 Step 6: Start Nexus Node

Replace `xxxxx` with your Node ID:

```bash
nexus-network start --node-id xxxxx
```

## 🔧 Troubleshooting (Node Not Appearing)

```bash
nexus-network register-user --wallet-address <YOUR_WALLET>
nexus-network register-node
nexus-network start
```

## 🧰 Optional Setup for Local Ubuntu

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential clang make gcc pkg-config libssl-dev curl wget
```

### Optional: Install Rust

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

## 🔁 Update Nexus CLI

Re-run this anytime to update:

```bash
curl https://cli.nexus.xyz/ | sh
```

## 🔓 Open Ports

Make sure the following ports are open:

- TCP 443  
- TCP 8443  


## 🔁 Update Nexus CLI (v0.9.4)

If you're already running a node and want to upgrade to the latest version:

### 🖥 Ubuntu 22.04:

```bash
screen -r nexus
```

> Press `Q` to stop the run

```bash
curl https://cli.nexus.xyz/ | sh
source /root/.profile
nexus-network start --node-id YOUR_ID
```

### 🧪 Ubuntu 24.04:

```bash
screen -r nexus
```

> Press `Q` to stop the run

```bash
curl https://cli.nexus.xyz/ | sh
source ~/.bashrc
nexus-network start --node-id YOUR_ID
```


## 🧪 Quick Commands Summary

| Command                                                   | Description                         |
|-----------------------------------------------------------|-------------------------------------|
| `curl https://cli.nexus.xyz/ \| sh`                       | Install or update Nexus CLI         |
| `source /root/.profile`                                   | Load Nexus CLI into shell           |
| `nexus-network start --node-id <NODE_ID>`                 | Start Nexus node                    |
| `nexus-network register-user --wallet-address <WALLET>`   | Register wallet                     |
| `nexus-network register-node`                             | Register node                       |
| `nexus-network logout`                                    | Logout from CLI                     |


